_NOTE: This release is under development and not yet published._

# What's notqmail?

It's software for running an email server. See [[our wiki|Home]] for more information.


# What's new?

This release of notqmail is guided by two themes: **fix bugs** and **reduce bug likelihood**.

## Fix bugs

- [Vulnerabilities we've inherited from qmail 1.03, reported by Qualys](https://www.qualys.com/2020/05/19/cve-2005-1513/remote-code-execution-qmail.txt). ([#133](https://github.com/notqmail/notqmail/pull/133))
    - [CVE-2005-1515](http://cve.circl.lu/cve/CVE-2005-1515): fix signedness wraparound in `substdio_{put,bput}()`.
    - [CVE-2005-1514](http://cve.circl.lu/cve/CVE-2005-1514): fix possible signed integer overflow in `commands()`.
    - [CVE-2005-1513](http://cve.circl.lu/cve/CVE-2005-1513): fix integer overflow in `stralloc_readyplus()`.
    - Fix several other places where variables could overflow.
- `qmail-pop3d`: instead of running as root if root authenticates (and being a vector for a dictionary attack on the root password), exit 1 to look just like a failed `checkpassword` login. ([#92](https://github.com/notqmail/notqmail/pull/92))
- `qmail-inject`: do not parse header recipients if `-a` is given. ([#8](https://github.com/notqmail/notqmail/pull/8))
- Correctly detect multiple IP addresses on the same interface. ([#96](https://github.com/notqmail/notqmail/pull/96))
- Remove workaround for ancient DNS servers that do not properly support CNAME. [Patch by Jonathan de Boyne Pollard](https://jdebp.eu/Softwares/djbwares/qmail-patches.html#any-to-cname) that was floating around the net for years. ([#97](https://github.com/notqmail/notqmail/pull/97))
- Fix possible integer overflow in `alloc()`. ([#109](https://github.com/notqmail/notqmail/pull/109))

## Reduce bug likelihood

- Remove `dnscname` and `dnsmxip` programs that were being built but not installed. ([#69](https://github.com/notqmail/notqmail/pull/69))
- Remove `systype` and related platform detection. ([#34](https://github.com/notqmail/notqmail/pull/34))
- Remove unused variable in `maildir.c`. ([#78](https://github.com/notqmail/notqmail/pull/78))
- Reduce variable scope in `tcpto.c`. ([#111](https://github.com/notqmail/notqmail/pull/111))
- Avoid local variables shadowing same-named globals. ([#113](https://github.com/notqmail/notqmail/pull/113))
- Avoid needing `exit.h` in named-pipe bug check. ([#108](https://github.com/notqmail/notqmail/pull/108))
- Add a `test` target and some unit tests, using [Check](https://libcheck.github.io/check/doc/check_html/index.html#Top). ([#102](https://github.com/notqmail/notqmail/pull/102))
- Add missing function declarations in `cdbmss.h`, `scan.h`. ([#64](https://github.com/notqmail/notqmail/pull/64))
- Add missing return types to `main()`. ([#85](https://github.com/notqmail/notqmail/pull/85))
- Add `hier.h` for inclusion in `instcheck.c`, `instchown.c`, `instpackage.c`. ([#64](https://github.com/notqmail/notqmail/pull/64))
- Use system headers and types instead of the `HASSHORTSETGROUPS` check. ([#72](https://github.com/notqmail/notqmail/pull/72))
- Use system headers instead of redeclaring `exit()`, `read()`, `write()`, `malloc()`, `free()`, `fork()`, `uint32_t`. ([#79](https://github.com/notqmail/notqmail/pull/79), [#80](https://github.com/notqmail/notqmail/pull/80), [#81](https://github.com/notqmail/notqmail/pull/81), [#82](https://github.com/notqmail/notqmail/pull/82), [#101](https://github.com/notqmail/notqmail/pull/101), [#30](https://github.com/notqmail/notqmail/pull/30))

## Other changes

- Remove DJB's TODO. ([#68](https://github.com/notqmail/notqmail/pull/68))
- Replace many `pobox.com` URLs. ([#54](https://github.com/notqmail/notqmail/pull/54))
- Acknowledge [Erik Sjölund](https://github.com/eriksjolund)'s `qmail-local.c` bugfix that we've inherited from netqmail. ([#118](https://github.com/notqmail/notqmail/pull/118))
- TravisCI: move setting `MAKEFLAGS` out of the script and into the matrix. ([#58](https://github.com/notqmail/notqmail/pull/58))
- Avoid generating catted manpages by building with `NROFF=true`. ([#116](https://github.com/notqmail/notqmail/pull/116))
- Optionally create a `systemd` service file. ([#114](https://github.com/notqmail/notqmail/pull/114))
- Run an alternate `qmail-remote` by setting `QMAILREMOTE` in `qmail-send`'s environment. ([#46](https://github.com/notqmail/notqmail/pull/46))

## Intent to remove

In the course of developing this release, we found programs that we intend to remove in the next release. We believe none of these remains necessary or useful enough to be worth the cost of maintaining. If you disagree, please let us know!

- Remove `qsmhook`, long since replaced by `preline`. ([#87](https://github.com/notqmail/notqmail/pull/87))
- Remove inefficient `maildirwatch`. ([#93](https://github.com/notqmail/notqmail/pull/93))
- Remove obsolete mail client wrappers. ([#99](https://github.com/notqmail/notqmail/pull/99))
- Remove `qmail-pop3d`, since Maildir is well supported by actively maintained POP3 servers (e.g., [Courier IMAP](https://www.courier-mta.org/imap/) or [Dovecot](https://www.dovecot.org/)).


## Thanks

We thank Qualys for their findings, collaborative approach, and impetus to cut a new release. 


## GitHub references

- All [closed 1.08 issues](https://github.com/notqmail/notqmail/issues?q=is%3Aissue+is%3Aclosed+milestone%3A1.08)
- All [closed 1.08 PRs](https://github.com/notqmail/notqmail/pulls?q=is%3Apr+is%3Aclosed+milestone%3A1.08)


# How to install

See [[Install]].


# Getting help

See [[Help]].