[[!meta title="Designs"]]

One way to try to summarize where we're headed:

> By following qmail's design principles more consistently, modern features will become easy to add.

Here are some sketches for how we can get features by making qmail more like itself.


## Port 587 (IPv6 and) mandatory STARTTLS and AUTH

We can follow and extend the design of qmail's POP3 service.
Amitai has been running (a slightly more complicated version of) this in production for a couple years.

1. Import some of [acceptutils](https://schmonz.com/software/acceptutils/):
    - For SMTP AUTH and TLS, import `qmail-authup`
        - Also supersedes `qmail-popup`; make that a one-line compatibility wrapper
		- (We drop APOP support, that's all)
		- (SMTP AUTH supports PLAIN and LOGIN only, no CRAM-MD5)
    - For ensuring root can't pass `checkpassword`, import `checknotroot`
3. Import mess822's `ofmipd` as `qmail-ofmipd`
    - Share code with `qmail-smtpd`, where sensible
4. In `qmail-ofmipd`, add logic for when `AUTHUP_USER` is set

Then run under [ucspi-ssl](https://www.fehcom.de/ipnet/ucspi-ssl.html)'s `sslserver -n`, configured like so:

[[!format sh """
exec 2>&1
exec env                                       \
    UCSPITLS='!'                               \
    SSL_UID=$(id -u ucspissl)                  \
    SSL_GID=$(id -g ucspissl)                  \
    CERTFILE=/var/qmail/control/servercert.pem \
    sslserver -ne -vRl0                        \
    0 587                                      \
    qmail-authup smtp                          \
    checkpassword                              \
    checknotroot                               \
    qmail-ofmipd
"""]]

SSL processing runs as the `ucspissl` user.
`qmail-ofmipd` runs as the authenticated user.

Alternatively, [s6-networking](https://www.skarnet.org/software/s6-networking/)'s `s6-tcpserver` and `s6-ucspitlsd` can be configured similarly. Both `sslserver` and `s6-tcpserver` support IPv6.


## Port 110 (IPv6 and) mandatory STARTTLS and AUTH

1. Replace `tcpserver` with `sslserver -n` (or `s6-tcpserver` and `s6-ucspitlsd`), as above.
2. Set `UCSPITLS=!`, as above.

SSL processing runs as the `ucspissl` user.
`qmail-pop3d` contines to run as the authenticated user.


## Port 25 (IPv6 and) opportunistic STARTTLS

Amitai has been running (a slightly more complicated version of) this in production for a couple years.

1. In `qmail-smtpd`, implement the very small UCSPI-TLS interface
	- Share or borrow from `qmail-authup`
2. Add a tiny bit of logic for TLS state

Then run `sslserver -n` (or `s6-tcpserver` and `s6-ucspitlsd`), configured like so:

[[!format sh """
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
"""]]

SSL processing runs as the `ucspissl` user.
`qmail-smtpd` continues to run as `qmaild`.


## Outbound STARTTLS, AUTH, IPv6, etc.

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

Our next move is to take advantage of s6-networking's `s6-ucspitlsc` (or `sslclient -y`, a delayed-encryption mode analogous to `sslserver -n`, which was present in [Scott Gifford's original UCSPI-TLS patch](https://github.com/SuperScript/ucspi-ssl/compare/master...scottgifford:master) and which Erwin Hoffmann has agreed to merge into a future ucspi-ssl.)
We port the [inoa.net TLS patch](http://inoa.net/qmail-tls/)'s `qmail-remote` logic to `qmail-smtpc`.
Iff we negotiate `STARTTLS`, then we notify `s6-ucspitlsc` (or `sslclient`) to start encryption via the UCSPI-TLS interface.
Since TCP and SSL are handled by an external program, we should be able to express the patch's logic with much less (and much more obvious) code.

Once we import its `update_tmprsadh` script, we have equivalent and compatible functionality to the TLS patch in `qmail-smtpd` and `qmail-remote` (and `qmail-ofmipd`, too).
Users can simply stop applying the patch.
They won't even have to move their certs or change their `cron` jobs.

We can merge again here.


### 3. Add EHLO parsing

We're making good progress, and we're about to add a bunch more capabilities.
It's time for a
standardized EHLO parser ([[!template id=pr number=173]]).


### 4. Add AUTH

Next, we pick a sufficiently configurable outbound AUTH patch and apply it to `qmail-smtpc`.

We can merge again here.


### 5. Add SIZE and PIPELINING

We apply [DerDakon's patch](https://opensource.sf-tec.de/qmail/qmail-remote-ESMTP-0.05.diff) to `qmail-smtpc`, and can merge again here.


### 6. Add SMTPUTF8

This is the only other popular and small `qmail-remote` patch we currently know of.
Apply it, or an independent implementation, to `qmail-smtpc` (and also to `qmail-smtpd` and `qmail-ofmipd`).

We can merge again here, and can consider moving `qmail-newremote` to `qmail-remote`.


### 7. Add IPv6

`sslclient` and `s6-tcpclient` support v6 transport.
Do `qmail-remote`'s DNS-lookup routines support v6 transport and/or responses?
If not, now's the time to switch to a djbdns-derived or -inspired DNS API that supports both.

We can merge again here, and if we haven't already done so, can again consider moving `qmail-newremote` to `qmail-remote`.


## SRS and DKIM

### 1. Import [qmail-qfilter](https://untroubled.org/qmail-qfilter/)

- For a `QMAILQUEUE` wrapper that runs `qmail-qfilter` with the sequence of Unix filters listed in `control/smtpfilters`, rejecting if any of them reject, import `qmail-qfilter-queue` from rejectutils
- For a Unix filter that prepends a `Received:` header with TLS connection details, import `qmail-qfilter-addtlsheader` from acceptutils
    - (So maybe we should import `qmail-qfilter` and `qmail-qfilter-queue` sooner as part of TLS, above)
- To let filters provide meaningful error strings, maybe merge the [qmail-queue-custom-error patch](https://notes.sagredo.eu/files/qmail/patches/qmail-queue-custom-error-v2.netqmail-1.05.patch)

### 2. Run inbound messages through new Unix filters

- Write `qmail-qfilter-srsreverse` to SRS-unwrap envelope senders
    - List it in `control/smtpfilters`
- Write `qmail-qfilter-dkimverify` to verify DKIM signatures
    - List it in `control/smtpfilters` -- order doesn't matter as long as filters do not modify anything before DKIM-Signature header

### 3. Write `qmail-rfilter` and friends

- Write `qmail-rfilter`, which is to `qmail-remote` as `qmail-qfilter` is to `qmail-queue`: an easy way to run Unix filters on outbound messages
- Write `qmail-rfilter-remote`, a `QMAILREMOTE` wrapper that runs `qmail-rfilter` with the sequence of Unix filters in `control/remotefilters` (akin to `qmail-qfilter-queue` for `QMAILQUEUE`). qmail-rfilter-remote should ultimately call qmail-remote. But qmail-remote will use fd 0 to read the message. This will the original message in the queue/mess directory. So to make the filters effective, we need to use either of the two method
    - pipe the output of the filters to qmail-remote. This will mean using pipe() and fork() where qmail-remote runs as a child process
    - create a new file. Dup the fd to 1 and then call the filters. Once the filters have finished, reopen the file and dup the fd to 0 and then do exec of qmail-remote with the same arguments that qmail-rspawn called qmail-rfilter-local.

- Write `qmail-lfilter-local`, a `QMAILLOCAL` wrapper that runs `qmail-lfilter` with the sequence of Unix filters in
`control/localfilters` (akin to `qmail-qfilter-queue` for `QMAILQUEUE`). qmail-lfilter-remote should ultimately call qmail-local. But qmail-local will use fd 0 to read the message. This will be the original message in the queue/mess directory. So to make the filters effective, we need to use either of the two method
    - pipe the output of the filters to qmail-local. This will mean using pipe() and fork() where qmail-local runs as a child process
    - create a new file. Dup the fd to 1 and then call the filters. Once the filters have finished, reopen the file and dup the fd to 0 and then do exec of qmail-local with the same arguments that qmail-lspawn called qmail-lfilter-local.

### 4. Run outbound messages through new Unix filters

- Write `qmail-rfilter-srsforward`, a Unix filter that SRS-rewrites envelope senders
    - List it in `control/remotefilters`
- Write `qmail-rfilter-dkimsign`, a Unix filter that signs messages with DKIM
    - List it `control/remotefilters` -- This needs to be last if any of the filters are going to modify the modify or the headers (h=) that will be used for DKIM signing.
