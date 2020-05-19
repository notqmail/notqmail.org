_NOTE: This release is under development and not yet published._

# What's notqmail?

It's software for running an email server. See [[our wiki|Home]] for more information.


# What's new?

This release of notqmail is guided by two themes: **fix bugs** and **reduce bug likelihood**.

## Fix bugs

- [Vulnerabilities in qmail 1.03 reported by Qualys](https://www.qualys.com/2020/05/19/cve-2005-1513/remote-code-execution-qmail.txt). ([#133](https://github.com/notqmail/notqmail/pull/133))
- `qmail-inject`: do not parse header recipients if `-a` is given. ([#8](https://github.com/notqmail/notqmail/pull/8))
- Correctly detect multiple IP addresses on the same interface. ([#96](https://github.com/notqmail/notqmail/pull/96))
- Remove workaround for ancient DNS servers that do not properly support CNAME. Patch by Jonathan de Boyne Pollard that was floating around the net for years. ([#97](https://github.com/notqmail/notqmail/pull/97))
- Fix possible integer overflow in `alloc()`. ([#109](https://github.com/notqmail/notqmail/pull/109))

## Reduce bug likelihood

- Remove `systype` and attendant platform detection. ([#34](https://github.com/notqmail/notqmail/pull/34))
- TravisCI: move setting `MAKEFLAGS` out of the script and into the matrix. ([#58](https://github.com/notqmail/notqmail/pull/58))
- Add missing function declarations in `cdbmss.h`, `scan.h`. ([#64](https://github.com/notqmail/notqmail/pull/64))
- Create `hier.h` to include in `instcheck.c`, `instchown.c`, `instpackage.c`. ([#64](https://github.com/notqmail/notqmail/pull/64))
- Remove `dnscname` and `dnsmxip` binaries that were only present in the build tree, but not installed. ([#69](https://github.com/notqmail/notqmail/pull/69))
- Remove unused variable `r` in `maildir.c`. ([#78](https://github.com/notqmail/notqmail/pull/78))
- Include `<unistd.h>` in `exit.h` instead of redeclaring `exit()`. ([#79](https://github.com/notqmail/notqmail/pull/79))
- Include `<unistd.h>` in `readwrite.h` instead of redeclaring `read()` and `write()`. ([#80](https://github.com/notqmail/notqmail/pull/80))
- Include `<stdlib.h>` in `alloc.c` instead of redeclaring `malloc()` and `free()`. ([#81](https://github.com/notqmail/notqmail/pull/81))
- Include `<sys/types.h>`, `<unistd.h>` in `fork.h`. ([#82](https://github.com/notqmail/notqmail/pull/82))
- Use `<stdint.h>` to get a really portable 32 bit unsigned type. ([#30](https://github.com/notqmail/notqmail/pull/30))
- Use system headers for files introduced since netqmail-1.06. ([#101](https://github.com/notqmail/notqmail/pull/101))
- Add missing return types to `main()`. ([#85](https://github.com/notqmail/notqmail/pull/85))
- Move some variables to a more local scope. ([#111](https://github.com/notqmail/notqmail/pull/111))
- Remove the need for `exit.h` in named pipe bug check. ([#108](https://github.com/notqmail/notqmail/pull/108))
- Rename local variables shadowing global variables of the same name. ([#113](https://github.com/notqmail/notqmail/pull/113))
- Remove `HASSHORTSETGROUPS` test, use system headers and types instead. ([#72](https://github.com/notqmail/notqmail/pull/72))
- Add a `test` target and one unit test, using [Check](https://libcheck.github.io/check/doc/check_html/index.html#Top). ([#102](https://github.com/notqmail/notqmail/pull/102))

## Other changes

- Add acknowledgement for the bugfix contribution from [Erik Sjölund](https://github.com/eriksjolund) to `qmail-local.c` that was included in netqmail. ([#118](https://github.com/notqmail/notqmail/pull/118))
- Allow to pass `NROFF=true` to `Makefile` to prevent installation of catted manpages. ([#116](https://github.com/notqmail/notqmail/pull/116))
- Remove DJB's TODO. ([#68](https://github.com/notqmail/notqmail/pull/68))
- Replace many `pobox.com` URLs. ([#54](https://github.com/notqmail/notqmail/pull/54))
- Optionally create a `systemd` service file. ([#114](https://github.com/notqmail/notqmail/pull/114))
- Run alternate `qmail-remote` by setting `QMAILREMOTE`. ([#46](https://github.com/notqmail/notqmail/pull/46))

## Intent to remove

In the course of developing this release, we found programs that we intend to remove in the next release. We believe none of these remains necessary or useful enough to be worth the cost of maintaining. If you disagree, please let us know!

- Remove `qsmhook`, long since replaced by `preline`. ([#87](https://github.com/notqmail/notqmail/pull/87))
- Remove inefficient `maildirwatch`. ([#93](https://github.com/notqmail/notqmail/pull/93))
- Remove obsolete mail client wrappers. ([#99](https://github.com/notqmail/notqmail/pull/99))
- Remove `qmail-pop3d`, since Maildir is well supported by actively maintained POP3 servers (e.g. [Courier IMAP](https://www.courier-mta.org/imap/) or [Dovecot](https://www.dovecot.org/)).

## GitHub references

- All [closed 1.08 issues](https://github.com/notqmail/notqmail/issues?q=is%3Aissue+is%3Aclosed+milestone%3A1.08)
- All [closed 1.08 PRs](https://github.com/notqmail/notqmail/pulls?q=is%3Apr+is%3Aclosed+milestone%3A1.08)


# How to install

See [[Install]].


# Getting help

See [[Help]].