# What is notqmail?

_It's not qmail. It's also not netqmail._

We all use email, so we all use email servers. notqmail is software for running an [email server](https://en.wikipedia.org/wiki/Message_transfer_agent). Someday, if we do a good job, some of the many [articles about how and why to run your own](https://arstechnica.com/information-technology/2014/02/how-to-run-your-own-e-mail-server-with-your-own-domain-part-1/) will recommend notqmail.

[notqmail](http://notqmail.org) is a community-driven fork of [qmail](https://cr.yp.to/qmail.html), beginning where [netqmail](http://netqmail.org) left off: providing stable, compatible, small releases to which existing qmail users can safely update. notqmail also aims higher: developing an extensible, easily packaged, and increasingly useful modern mail server.

_NOTE: This release is under development and not yet published._

## What's New

This initial 1.07 release of notqmail is guided by two themes: **fix broken builds** and **make packaging easier**.

### Fix broken builds

- [#24](https://github.com/notqmail/notqmail/pull/24), [#29](https://github.com/notqmail/notqmail/pull/29), [#57](https://github.com/notqmail/notqmail/pull/57): Support [utmpx](https://en.wikipedia.org/wiki/Utmp) in [qbiff(1)](https://github.com/notqmail/notqmail/blob/master/qbiff.1) for systems that no longer provide utmp.
- [#16](https://github.com/notqmail/notqmail/pull/16): Append `.md` extensions to [INSTALL](https://github.com/notqmail/notqmail/blob/master/INSTALL.md) and [SENDMAIL](https://github.com/notqmail/notqmail/blob/master/SENDMAIL.md) to disambiguate from `install` and `sendmail` on case-insensitive filesystems, such as HFS+.
- [#16](https://github.com/notqmail/notqmail/pull/16): Enable BIND 8 API compatibility for systems with BIND 9 resolvers.
- [#16](https://github.com/notqmail/notqmail/pull/16): Work around macOS linker error by explicitly initializing a struct.
- [#1](https://github.com/notqmail/notqmail/pull/1), [#20](https://github.com/notqmail/notqmail/pull/20), [#31](https://github.com/notqmail/notqmail/pull/31), [#53](https://github.com/notqmail/notqmail/pull/53), [#55](https://github.com/notqmail/notqmail/pull/55): Add missing function arguments, includes, and Makefile dependencies.

### Make packaging easier

- Fix builds on at least FreeBSD and macOS.
- [#15](https://github.com/notqmail/notqmail/pull/15): Look up qmail's UIDs and GIDs at run time, not build time.
- [#15](https://github.com/notqmail/notqmail/pull/15): Optionally build as non-root.
- [#4](https://github.com/notqmail/notqmail/pull/4): Optionally install as non-root, to a staging area, with DESTDIR.

### Other changes

- [#19](https://github.com/notqmail/notqmail/pull/19): Add TravisCI config.
- [#25](https://github.com/notqmail/notqmail/pull/25) Add `.gitignore`.
- [#15](https://github.com/notqmail/notqmail/pull/15): Remove [precompiled var-qmail package](https://cr.yp.to/qmail/var-qmail.html) support.
- [#27](https://github.com/notqmail/notqmail/pull/27): Remove `shar` target and `FILES`.
- [#33](https://github.com/notqmail/notqmail/pull/33): Remove `SYSDEPS`.
- [#38](https://github.com/notqmail/notqmail/pull/38): Remove `vfork()`, fixing macOS runtime.
- [#39](https://github.com/notqmail/notqmail/pull/39), [#42](https://github.com/notqmail/notqmail/pull/42): Update documents and URLs for notqmail.

### GitHub references

- All [closed 1.07 issues](https://github.com/notqmail/notqmail/issues?q=is%3Aissue+is%3Aclosed+milestone%3A1.07)
- All [closed 1.07 PRs](https://github.com/notqmail/notqmail/pulls?q=is%3Apr+is%3Aclosed+milestone%3A1.07)

## How to install

### On a single host

[Life with qmail](http://www.lifewithqmail.org/lwq.html#installation) continues to apply. Note that some modern systems — we've seen at least OpenBSD, FreeBSD, and Void Linux — don't provide `nroff`. [GNU troff](https://www.gnu.org/software/groff/) (aka `groff`) should do the trick.

### On many hosts

notqmail makes it easy to build once, install many.

#### On the build host

Customize `conf-users` and `conf-groups`, if needed, and note the names. Then build, stage, and create a tarball:

    $ make it man
    $ export DESTDIR=/path/to/staging/directory
    $ make package
    $ tar -C ${DESTDIR} -czf notqmail-1.07.tar.gz .


#### On an install host

Copy over `notqmail-1.07.tar.gz`, `instchown`, and `instcheck` from the build host. Extract the tarball -- e.g., with GNU Tar:

    # tar -C / --no-overwrite-dir -xzf notqmail-1.07.tar.gz

[Create users and groups](https://github.com/notqmail/notqmail/blob/master/INSTALL.ids) with names to match the build. Set permissions on installed files:

    # ./instchown

Then verify the installation, just as with a traditional qmail install:

    # ./instcheck