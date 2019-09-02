_NOTE: This release is under development and not yet published._

# What is notqmail?

_It's not qmail. It's also not netqmail._

# What's new?

## Intent to remove

- Remove qsmhook, long since replaced by preline. ([#87](https://github.com/notqmail/notqmail/pull/87))
- Remove inefficient maildirwatch. ([#93](https://github.com/notqmail/notqmail/pull/93))
- Remove obsolete mail client wrappers. ([#99](https://github.com/notqmail/notqmail/pull/99))

## Extension interface preview

- Run alternate qmail-remote by setting QMAILREMOTE. ([#46](https://github.com/notqmail/notqmail/pull/46))

## Other changes

- remove systype and attendant platform detection ([#34](https://github.com/notqmail/notqmail/pull/34))
- TravisCI: move setting MAKEFLAGS out of the script and in to the matrix. ([#58](https://github.com/notqmail/notqmail/pull/58))
- add missing function declarations in cdbmss.h, scan.h ([#64](https://github.com/notqmail/notqmail/pull/64))
- create hier.h to include in instcheck.c, instchown.c, instpackage.c ([#64](https://github.com/notqmail/notqmail/pull/64))
- remove dnscname and dnsmxip ([#69](https://github.com/notqmail/notqmail/pull/69))
- remove unused variable r in maildir.c. ([#78](https://github.com/notqmail/notqmail/pull/78))
- include unistd.h in readwrite.h. ([#80](https://github.com/notqmail/notqmail/pull/80))
- include stdlib.h in alloc.c. ([#81](https://github.com/notqmail/notqmail/pull/81))
- include sys/types.h, unistd.h in fork.h. ([#82](https://github.com/notqmail/notqmail/pull/82))
- remove TODO. ([#68](https://github.com/notqmail/notqmail/pull/68))

## GitHub references

- All [closed 1.08 issues](https://github.com/notqmail/notqmail/issues?q=is%3Aissue+is%3Aclosed+milestone%3A1.08)
- All [closed 1.08 PRs](https://github.com/notqmail/notqmail/pulls?q=is%3Apr+is%3Aclosed+milestone%3A1.08)