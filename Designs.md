# Designs

One way to try to summarize where we're headed:

> By following qmail's design principles more consistently, modern features will become easy to add.

Here are some sketches for how we can get features by making qmail more like itself.


## 1.09: SMTP recipient validation

The [RCPTCHECK patch](http://www.soffian.org/downloads/qmail/qmail-smtpd-doc.html) to `qmail-smtpd` is just enough interface for external programs to validate recipients.
Later, we may want the much more general [qmail-spp patch](http://qmail-spp.sourceforge.net/doc/).
Amitai (via pkgsrc) used to run the former and migrated easily to the latter.

1. Import some of [rejectutils](https://schmonz.com/qmail/rejectutils/):
    - For `control/rcptchecks` to be an admin-configurable sequence of RCPTCHECK-compatible programs, rejecting if any of them reject, import `qmail-rcptcheck`
        - This insulates users from our choice of RCPTCHECK or qmail-spp, as it runs equally well under either
    - For a recommended default checker, import `qmail-rcptcheck-realrcptto`, which is a RCPTCHECK-compatible program derived from [Paul Jarc's realrcptto patch](http://code.dogmap.org./qmail/#realrcptto) 
        - Far from meeting everyone's needs, but no false positives and will start to help
        - Duplicates delivery logic from several qmail programs
        - Later, with sufficient test coverage, we'll want to refactor to reduce duplication
    - For optional additional checkers, maybe import `qmail-rcptcheck-badrcptto` and `qmail-rcptcheck-qregex`


## Post-1.09: SPF

1. Switch from RCPTCHECK to qmail-spp (or maybe keep both)
2. Import [qmail-spp-spf](https://www.caputo.com/foss/qmail-spp-spf/)


## Post-1.09: Port 587 (IPv6 and) mandatory STARTTLS and AUTH

We can follow and extend the design of qmail's POP3 service.
Amitai has been running (a slightly more complicated version of) this in production for a couple years.

1. Import some of [acceptutils](https://schmonz.com/qmail/acceptutils/):
    - For SMTP AUTH and TLS, import `qmail-authup`
        - Also supersedes `qmail-popup`; make that a one-line compatibility wrapper
		- (We drop APOP support, that's all)
		- (SMTP AUTH supports PLAIN and LOGIN only, no CRAM-MD5)
    - For retrying failed logins, maybe import `qmail-reup`
    - For ensuring root can't pass `checkpassword`, import `checknotroot`
3. Import mess822's `ofmipd` as `qmail-ofmipd`
    - Share code with `qmail-smtpd`, where sensible
4. In `qmail-ofmipd`, add logic for when `AUTHUP_USER` is set

Then run under [ucspi-ssl](https://www.fehcom.de/ipnet/ucspi-ssl.html)'s `sslserver -n`, configured like so:

```sh
exec 2>&1
exec env                                       \
    UCSPITLS='!'                               \
    SSL_UID=$(id -u ucspissl)                  \
    SSL_GID=$(id -g ucspissl)                  \
    CERTFILE=/var/qmail/control/servercert.pem \
    sslserver -ne -vRl0                        \
    0 587                                      \
    qmail-reup -t 5                            \
    qmail-authup smtp                          \
    checkpassword                              \
    checknotroot                               \
    qmail-ofmipd
```

SSL processing runs as the `ucspissl` user.
`qmail-ofmipd` runs as the authenticated user.

`sslserver` supports IPv6.

At the time of writing, UCSPI-TLS support is being actively developed for [s6-networking](https://www.skarnet.org/software/s6-networking/), which also supports TLS and IPv6.
When it ships, `s6-ucspitlsd` can be used in place of `sslserver -n`.


## Post-1.09: Port 110 (IPv6 and) mandatory STARTTLS and AUTH

1. Replace `tcpserver` with `sslserver -n` (or `s6-ucspitlsd`), as above.
2. Set `UCSPITLS=!`, as above.

SSL processing runs as the `ucspissl` user.
`qmail-pop3d` contines to run as the authenticated user.


## Post-1.09: Port 25 (IPv6 and) opportunistic STARTTLS

Amitai has been running (a slightly more complicated version of) this in production for a couple years.

1. In `qmail-smtpd`, implement the very small UCSPI-TLS interface
	- Share or borrow from `qmail-authup`
2. Add a tiny bit of logic for TLS state

Then run `sslserver -n` (or `s6-ucspitlsd`), configured like so:

```sh
exec 2>&1
exec env                                       \
    UCSPITLS=''                                \
    SSL_UID=$(id -u ucspissl)                  \
    SSL_GID=$(id -g ucspissl)                  \
    CERTFILE=/var/qmail/control/servercert.pem \
    sslserver -ne -vRl0                        \
    -u $(id -u qmaild) -g $(id -g qmaild)      \
    0 25                                       \
    rblsmtpd -r zen.spamhaus.org               \
    qmail-smtpd
```

SSL processing runs as the `ucspissl` user.
`qmail-smtpd` continues to run as `qmaild`.


## Post-1.09: Outbound STARTTLS, AUTH, IPv6, etc.

`qmail-smtpd` is easily adapted (and tested) to new needs because it has no networking code.
By giving `qmail-remote` a matching design, we can give it the same properties.
[qremote](https://mojzis.com/software/qremote/) proves (a slightly more complicated version of) the concept.


### 1. Remove network code

- Extract SMTP client to `qmail-smtpc`
- Have `qmail-remote` run it with `tcpclient`

Within the notqmail codebase, this is a sweet refactoring -- not even introducing a new dependency, since we already require `tcpserver` or the equivalent.
But in a world where everyone still needs to patch notqmail, this is not a refactoring: all the popular patches will break.
If we want to merge here, we'll temporarily call it `qmail-newremote`.


### 2. Add STARTTLS

Our next move is to take advantage of `sslclient -y`, a delayed-encryption mode analogous to `sslserver -n`.
(Even though it doesn't exist at the time of writing, it's reasonable to posit its existence.
[Scott Gifford's original UCSPI-TLS patch](https://github.com/SuperScript/ucspi-ssl/compare/master...scottgifford:master) included it, and Erwin Hoffmann has agreed to merge it into ucspi-ssl.
Laurent Bercot is also actively working on UCSPI-TLS client support as `s6-ucspitlsc`.)
We port the [inoa.net TLS patch](http://inoa.net/qmail-tls/)'s `qmail-remote` logic to `qmail-smtpc`.
Iff we negotiate `STARTTLS`, then we notify `sslclient` (or `s6-ucspitlsc`) to start encryption via the UCSPI-TLS interface.
Since TCP and SSL are handled by an external program, we should be able to express the patch's logic with much less (and much more obvious) code.

Once we import its `update_tmprsadh` script, we have equivalent and compatible functionality to the TLS patch in `qmail-smtpd` and `qmail-remote` (and `qmail-ofmipd`, too).
Users can simply stop applying the patch.
They won't even have to move their certs or change their `cron` jobs.

We can merge again here.


### 3. Add AUTH

Next, we pick a sufficiently configurable outbound AUTH patch and apply it to `qmail-smtpc`.

We can merge again here.


### 4. Add SIZE and PIPELINING

We apply [DerDakon's patch](https://opensource.sf-tec.de/qmail/qmail-remote-ESMTP-0.05.diff) to `qmail-smtpc`, and can merge again here.


### 5. Add SMTPUTF8

This is the only other popular and small `qmail-remote` patch we currently know of.
Apply it, or an independent implementation, to `qmail-smtpc` (and also to `qmail-smtpd` and `qmail-ofmipd`).

We can merge again here, and can consider moving `qmail-newremote` to `qmail-remote`.


### 6. Add IPv6

`sslclient` and `s6-ucspitlsc` support v6 transport.
Do `qmail-remote`'s DNS-lookup routines support v6 transport and/or responses?
If not, now's the time to switch to a djbdns-derived or -inspired DNS API that supports both.

We can merge again here, and if we haven’t already done so, can again consider moving `qmail-newremote` to `qmail-remote`.


## Post-1.09: SRS and DKIM


### 1. Import `qmail-qfilter`

- For a `QMAILQUEUE` wrapper that runs `qmail-qfilter` with the sequence of Unix filters listed in `control/smtpfilters`, rejecting if any of them reject, import `qmail-qfilter-queue` from rejectutils
- For a Unix filter that prepends a `Received:` header with TLS connection details, import `qmail-qfilter-addtlsheader` from acceptutils
    - (So maybe we should import `qmail-qfilter` and `qmail-qfilter-queue` sooner as part of TLS, above)
- To let filters provide meaningful error strings, maybe merge the [qmail-queue-custom-error patch](https://notes.sagredo.eu/files/qmail/patches/qmail-queue-custom-error-v2.netqmail-1.05.patch)

### 2. Run inbound messages through new Unix filters

- Write `qmail-qfilter-srsreverse` to SRS-unwrap envelope senders
    - List it in `control/smtpfilters`
- Write `qmail-qfilter-dkimverify` to verify DKIM signatures
    - List it in `control/smtpfilters` -- probably needs to be first

### 3. Write `qmail-rfilter` and friends

- Write `qmail-rfilter`, which is to `qmail-remote` as `qmail-qfilter` is to `qmail-queue`: an easy way to run Unix filters on outbound messages
- Write `qmail-rfilter-remote`, a `QMAILREMOTE` wrapper that runs `qmail-rfilter` with the sequence of Unix filters in `control/remotefilters` (akin to `qmail-qfilter-queue` for `QMAILQUEUE`)

### 4. Run outbound messages through new Unix filters

- Write `qmail-rfilter-srsforward`, a Unix filter that SRS-rewrites envelope senders
    - List it in `control/remotefilters`
- Write `qmail-rfilter-dkimsign`, a Unix filter that signs messages with DKIM
    - List it `control/remotefilters` -- probably needs to be last
