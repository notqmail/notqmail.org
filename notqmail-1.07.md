# What is notqmail?

_It's not qmail. It's also not netqmail._

We all use email, so we all use email servers. notqmail is software for running an [email server](https://en.wikipedia.org/wiki/Message_transfer_agent). Someday, if we do a good job, some of the many [articles about how and why to run your own](https://arstechnica.com/information-technology/2014/02/how-to-run-your-own-e-mail-server-with-your-own-domain-part-1/) will recommend notqmail.

[notqmail](http://notqmail.org) is a community-driven fork of [qmail](https://cr.yp.to/qmail.html), beginning where [netqmail](http://netqmail.org) left off: providing stable, compatible, small releases to which existing qmail users can safely update. notqmail also aims higher: developing an extensible, easily packaged, and increasingly useful modern mail server.

_NOTE: This release is under development and not yet published._

## What's New

This initial 1.07 release of notqmail is guided by two themes:

### Fix broken builds

- Support utmpx in `qbiff(1)` for systems that no longer provide utmp.
- Append `.md` extensions to `INSTALL` and `SENDMAIL` to disambiguate from `install` and `sendmail` on case-insensitive filesystems, such as HFS+.
- Enable BIND 8 API compatibility for systems with BIND 9 resolvers.
- Work around macOS linker error by explicitly initializing a struct.
- Add missing function arguments, Makefile dependencies, and missing header files.

### Make packaging easier

- Fix builds on at least FreeBSD and macOS.
- Remove precompiled "var-qmail package" support.
- Look up qmail's UIDs and GIDs at run time, not build time.
- Optionally build as non-root.
- Optionally install as non-root, to a staging area, with DESTDIR.

### Other changes

- All [closed 1.07 issues](https://github.com/notqmail/notqmail/issues?q=is%3Aissue+is%3Aclosed+milestone%3A1.07)
- All [closed 1.07 PRs](https://github.com/notqmail/notqmail/pulls?q=is%3Apr+is%3Aclosed+milestone%3A1.07)

## How to install

The instructions for building and installing notqmail on a single host are unchanged from qmail's.

At least one assumption has changed in the intervening years: while `nroff` remains a non-optional build dependency, some systems have stopped providing it. We've seen this on at least OpenBSD, FreeBSD, and Void Linux. [GNU troff](https://www.gnu.org/software/groff/) (aka `groff`) should do the trick.

New in notqmail-1.07, it's easy to build a package on one machine and run it on others.

### On the build host:

Customize `conf-users` and `conf-groups`, if needed, and note the names. Then build, stage, and create a tarball:

    $ make it man
    $ export DESTDIR=/path/to/staging/directory
    $ make package
    $ tar -C ${DESTDIR} -czf notqmail-1.07.tar.gz .


### On the install host:

Copy over `notqmail-1.07.tar.gz`, `instchown`, and `instcheck` from the build host. Extract the tarball -- e.g., with GNU Tar:

    # tar -C / --no-overwrite-dir -xzf notqmail-1.07.tar.gz

[Create users and groups](https://github.com/notqmail/notqmail/blob/master/INSTALL.ids) with names to match the build. Set permissions on installed files, then verify the installation just as with a traditional qmail install:

    # ./instchown
    # ./instcheck