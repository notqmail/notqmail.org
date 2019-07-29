# What is notqmail?

_It's not qmail. It's also not netqmail._

We all use email, so we all use email servers. notqmail is software for running an [email server](https://en.wikipedia.org/wiki/Message_transfer_agent). Someday, if we do a good job, some of the many [articles about how and why to run your own](https://arstechnica.com/information-technology/2014/02/how-to-run-your-own-e-mail-server-with-your-own-domain-part-1/) will recommend notqmail.

[notqmail](http://notqmail.org) is a community-driven fork of [qmail](https://cr.yp.to/qmail.html). notqmail begins where [netqmail](http://netqmail.org) left off: providing stable, compatible, small releases to which existing qmail users can safely update. notqmail also aims higher: developing an extensible, easily packaged, and increasingly useful modern mail server.

_NOTE: This release is under development and not yet published._

## What's New

notqmail-1.07 supports staged installation, where build and packaging is done on one host for installation to another.  notqmail can be built and packaged without requiring qmail system accounts, or on a build host where the uid/gid values for those accounts differ from the install host.

notqmail-1.07 now builds on FreeBSD and Mac OS X.

* Staged installation
    * the setup target supports the `DESTDIR` environment variable for staged installation outside of `/var/qmail`.
    * a new target, `package`, will make a staged qmail install as a regular (non-root) user.
    * The program `instchown` is run on the install host to set file ownership and other root-required installation steps.
    * uid/gid lookup of qmail system accounts is now done at runtime.  
* Build platforms
    * FreeBSD: build on utmpx-only systems.
    * Mac OS X: build on case-insensitive filesystems, enable compatibility mode for name resolution, work around linker error.
* Correctness and cleanup
    * Add missing function arguments, Makefile dependencies, and missing header files.
    * Remove precompiled "var-qmail package" support.

All notqmail-1.07 [closed issues](https://github.com/notqmail/notqmail/issues?q=is%3Aissue+is%3Aclosed+milestone%3A1.07) and [closed PRs](https://github.com/notqmail/notqmail/pulls?q=is%3Apr+is%3Aclosed+milestone%3A1.07).

## How to install

The instructions for building and installing notqmail on a single host are unchanged from qmail's.

notqmail-1.07 also makes it easy to build a package on one machine and run it on others.

### On the build host:

Customize `conf-users` and `conf-groups`, if needed, and note the names. Then build, stage, and create a tarball:

    $ make it man
    $ export DESTDIR=/path/to/staging/directory
    $ make package
    $ tar -C ${DESTDIR} -czf notqmail-1.07.tar.gz .


### On the install host:

Copy over `notqmail-1.07.tar.gz`, `instchown`, and `instcheck` from the build host. Extract the tarball -- e.g., with GNU Tar:

    # tar -C / --no-overwrite-dir -xzf notqmail-1.07.tar.gz

Create users and groups with names to match the build. Then set permissions on installed files, and verify the installation just as with a traditional qmail install:

    # ./instchown
    # ./instcheck