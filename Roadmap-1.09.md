_NOTE: This release is under development and not yet published._

# What's notqmail?

It's software for running an email server. See [[our wiki|Home]] for more information.


# What's new?

This release of notqmail is guided by two themes: **fix more bugs** and **further reduce bug likelihood**.

## Fix more bugs

- ...

## Further reduce bug likelihood

- Remove obsolete mail client wrappers. ([#99](https://github.com/notqmail/notqmail/pull/99))

## Other changes

- ...

## Intent to remove

In 1.08, we announced our intent to remove the following programs:

- Remove `qsmhook`, long since replaced by `preline`. ([#87](https://github.com/notqmail/notqmail/pull/87))
- Remove inefficient `maildirwatch`. ([#93](https://github.com/notqmail/notqmail/pull/93))
- Remove `qmail-pop3d`, since Maildir is well supported by actively maintained POP3 servers (e.g., [Courier IMAP](https://www.courier-mta.org/imap/) or [Dovecot](https://www.dovecot.org/)).

In the course of developing this release, we found programs that we intend to remove in the next release. We believe none of these remains necessary or useful enough to be worth the cost of maintaining. If you disagree, please let us know!

- Remove code for QMTP and QMQP. ([#142](https://github.com/notqmail/notqmail/issues/142))

## GitHub references

- All [closed 1.09 issues](https://github.com/notqmail/notqmail/issues?q=is%3Aissue+is%3Aclosed+milestone%3A1.09)
- All [closed 1.09 PRs](https://github.com/notqmail/notqmail/pulls?q=is%3Apr+is%3Aclosed+milestone%3A1.09)


# How to install

See [[Install]].


# Getting help

See [[Help]].