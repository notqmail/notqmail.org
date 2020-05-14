_NOTE: This release is under development and not yet published._

# What's notqmail?

It's software for running an email server. See [[our wiki|Home]] for more information.

# What's new?

## Extension interface preview

- Run alternate qmail-remote by setting QMAILREMOTE. ([#46](https://github.com/notqmail/notqmail/pull/46))

## User visible bug fixes

- qmail-inject: do not parse header recipients if "-a" is given. ([#8](https://github.com/notqmail/notqmail/pull/8))
- correctly detect multiple IP addresses on the same interface. ([#96](https://github.com/notqmail/notqmail/pull/96))
- remove workaround for ancient DNS servers that do not properly support CNAME. Patch by Jonathan de Boyne Pollard that was floating around the net for years. ([#97](https://github.com/notqmail/notqmail/pull/97))
- fix possible integer overflow in alloc(). ([#109](https://github.com/notqmail/notqmail/pull/109))

## Other changes

- remove systype and attendant platform detection ([#34](https://github.com/notqmail/notqmail/pull/34))
- TravisCI: move setting MAKEFLAGS out of the script and in to the matrix. ([#58](https://github.com/notqmail/notqmail/pull/58))
- add missing function declarations in cdbmss.h, scan.h ([#64](https://github.com/notqmail/notqmail/pull/64))
- create hier.h to include in instcheck.c, instchown.c, instpackage.c ([#64](https://github.com/notqmail/notqmail/pull/64))
- remove dnscname and dnsmxip binaries that were only present in the build tree, but not installed ([#69](https://github.com/notqmail/notqmail/pull/69))
- remove unused variable r in maildir.c. ([#78](https://github.com/notqmail/notqmail/pull/78))
- include unistd.h in exit.h instead of redeclaring exit(). ([#79](https://github.com/notqmail/notqmail/pull/79))
- include unistd.h in readwrite.h instead of redeclaring read() and write(). ([#80](https://github.com/notqmail/notqmail/pull/80))
- include stdlib.h in alloc.c instead of redeclaring malloc() and free(). ([#81](https://github.com/notqmail/notqmail/pull/81))
- include sys/types.h, unistd.h in fork.h. ([#82](https://github.com/notqmail/notqmail/pull/82))
- remove TODO. ([#68](https://github.com/notqmail/notqmail/pull/68))
- use <stdint.h> to get a really portable 32 bit unsigned type. ([#30](https://github.com/notqmail/notqmail/pull/30))
- use system headers for files introduced since netqmail-1.06. ([#101](https://github.com/notqmail/notqmail/pull/101))
- add missing return types to main(). ([#85](https://github.com/notqmail/notqmail/pull/85))
- move some variables to a more local scope. ([#111](https://github.com/notqmail/notqmail/pull/111))
- replace many pobox.com URLs. ([#54](https://github.com/notqmail/notqmail/pull/54))
- optionally create a systemd service file. ([#114](https://github.com/notqmail/notqmail/pull/114))
- add acknowledgement for the bug fix contribution from @eriksjolund to qmail-local.c that was included in netqmail alread. ([#118](https://github.com/notqmail/notqmail/pull/118))
- remove the need for exit.h in named pipe bug check. ([#108](https://github.com/notqmail/notqmail/pull/108))
- rename local variables shadowing global variables of the same name. ([#113](https://github.com/notqmail/notqmail/pull/113))
- remove HASSHORTSETGROUPS test, use system headers and types instead. ([#72](https://github.com/notqmail/notqmail/pull/72))
- add a test target and one unit test, using [Check](https://libcheck.github.io/check/doc/check_html/index.html#Top). ([#102](https://github.com/notqmail/notqmail/pull/102))

## Intent to remove

In the course of developing this release, we found programs that we intend to remove in the next release. We believe none of these remains necessary or useful enough to be worth the cost of maintaining. If you disagree, please let us know!

- Remove qsmhook, long since replaced by preline. ([#87](https://github.com/notqmail/notqmail/pull/87))
- Remove inefficient maildirwatch. ([#93](https://github.com/notqmail/notqmail/pull/93))
- Remove obsolete mail client wrappers. ([#99](https://github.com/notqmail/notqmail/pull/99))

## GitHub references

- All [closed 1.08 issues](https://github.com/notqmail/notqmail/issues?q=is%3Aissue+is%3Aclosed+milestone%3A1.08)
- All [closed 1.08 PRs](https://github.com/notqmail/notqmail/pulls?q=is%3Apr+is%3Aclosed+milestone%3A1.08)