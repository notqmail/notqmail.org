# Designs

One way to try to summarize where we're headed:

> By following qmail's design principles more consistently, modern features will become easy to add.

Here are some sketches for how we can get features by making qmail more like itself.


## Port 587 (IPv6 and) mandatory STARTTLS and AUTH

We can follow and extend the design of qmail's POP3 service.
Amitai has been running (a slightly more complicated version of) this in production for a couple years.

1. Import some of acceptutils:
    - For SMTP AUTH and TLS, import `qmail-authup`
        - Also supersedes `qmail-popup`; make that a one-line compatibility wrapper
		- (We drop APOP support, that's all)
		- (SMTP AUTH supports PLAIN and LOGIN only, no CRAM-MD5)
    - For retrying failed logins, maybe import `qmail-reup`
    - For ensuring root can't pass `checkpassword`, import `checknotroot`
3. Import mess822's `ofmipd` as `qmail-ofmipd`
    - Share code with `qmail-smtpd`, where sensible
4. In `qmail-ofmipd`, add logic for when `AUTHUP_USER` is set

Then run under `sslserver -n`, configured like so:

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


## Port 110 (IPv6 and) mandatory STARTTLS and AUTH

1. Replace `tcpserver` with `sslserver -n`, as above.
2. Set `UCSPITLS=!`, as above.

SSL processing runs as the `ucspissl` user.
`qmail-pop3d` contines to run as the authenticated user.


## Port 25 (IPv6 and) opportunistic STARTTLS

Amitai has been running (a slightly more complicated version of) this in production for a couple years.

1. In `qmail-smtpd`, implement the very small UCSPI-TLS interface
	- Share or borrow from `qmail-authup`
2. Add a tiny bit of logic for TLS state

Then run `sslserver -n`, configured like so:

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


## Outbound STARTTLS, AUTH, IPv6, etc.

`qmail-smtpd` is easily adapted (and tested) to new needs because it has no networking code.
By giving `qmail-remote` a matching design, we can give it the same properties.
qremote proves (a slightly more complicated version of) the concept.


### 1. Remove network code

- Extract SMTP client to `qmail-rsmtp`
- Have `qmail-remote` run it with `tcpclient`

Within the notqmail codebase, this is a sweet refactoring -- not even introducing a new dependency, since we already require `tcpserver` or the equivalent.
But in a world where everyone still needs to patch notqmail, this is not a refactoring: all the popular patches will break.
If we want to merge here, we'll temporarily call it `qmail-newremote`.


### 2. Add STARTTLS

Our next move is to take advantage of `sslclient -y`, a delayed-encryption mode analogous to `sslserver -n`.
(Even though it doesn't exist at the time of writing, it's reasonable to posit its existence. Scott Gifford's original UCSPI-TLS patch included it, and the current ucspi-ssl maintainer has recently agreed to merge it.)
We port the inoa.net TLS patch's `qmail-remote` logic to `qmail-rsmtp`.
Iff we negotiate `STARTTLS`, then we notify `sslclient` to start encryption via the UCSPI-TLS interface.
Since TCP and SSL are handled by an external program, we should be able to express the patch's logic with much less (and much more obvious) code.

Once we import its `update_tmprsadh` script, we have equivalent and compatible functionality to the TLS patch in `qmail-smtpd` and `qmail-remote` (and `qmail-ofmipd`, too).
Users can simply stop applying the patch.
They won't even have to move their certs or change their `cron` jobs.

We can merge again here.


### 3. Add AUTH

Next, we pick a sufficiently configurable outbound AUTH patch and apply it to `qmail-rsmtp`.

We can merge again here.


### 4. Add SIZE

We apply @DerDakon's patch to `qmail-rsmtpd`, and can merge again here.


### 4. Add SMTPUTF8

This is the only other popular and small `qmail-remote` patch we currently know of.
Apply it to `qmail-rsmtpd` (and also to `qmail-smtpd` and `qmail-ofmipd`).

We can merge again here, and can consider moving `qmail-newremote` to `qmail-remote`.


### 4. Add IPv6

`sslclient` supports v6 transport.
Do `qmail-remote`'s DNS-lookup routines support v6 transport and/or responses?
If not, now's the time to switch to a djbdns-derived or -inspired DNS API that supports both.

We can merge again here, and if we haven't already done so, then it's definitively time to move `qmail-newremote` to `qmail-remote`.