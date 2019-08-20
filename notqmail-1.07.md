# What is notqmail?

_It's not qmail. It's also not netqmail._

We all use email, so we all use email servers. notqmail is software for running an [email server](https://en.wikipedia.org/wiki/Message_transfer_agent). Someday, if we do a good job, some of the many [articles about how and why to run your own](https://arstechnica.com/information-technology/2014/02/how-to-run-your-own-e-mail-server-with-your-own-domain-part-1/) will recommend notqmail.

[notqmail](http://notqmail.org) is a community-driven fork of [qmail](https://cr.yp.to/qmail.html), beginning where [netqmail](http://netqmail.org) left off: providing stable, compatible, small releases to which existing qmail users can safely update. notqmail also aims higher: developing an extensible, easily packaged, and increasingly useful modern mail server.


# What's new

This initial 1.07 release of notqmail is guided by two themes: **fix broken builds** and **make packaging easier**.

## Fix broken builds

- Support [utmpx](https://en.wikipedia.org/wiki/Utmp) in [qbiff(1)](https://github.com/notqmail/notqmail/blob/master/qbiff.1) for systems that no longer provide utmp. ([#24](https://github.com/notqmail/notqmail/pull/24), [#29](https://github.com/notqmail/notqmail/pull/29), [#57](https://github.com/notqmail/notqmail/pull/57)) 
- Append `.md` extensions to [INSTALL](https://github.com/notqmail/notqmail/blob/master/INSTALL.md) and [SENDMAIL](https://github.com/notqmail/notqmail/blob/master/SENDMAIL.md) to disambiguate from `install` and `sendmail` on case-insensitive filesystems, such as HFS+. ([#16](https://github.com/notqmail/notqmail/pull/16))
- Enable BIND 8 API compatibility for systems with BIND 9 resolvers. ([#16](https://github.com/notqmail/notqmail/pull/16))
- Work around macOS linker error by explicitly initializing a struct. ([#16](https://github.com/notqmail/notqmail/pull/16))
- Add missing function arguments, includes, and Makefile dependencies. ([#1](https://github.com/notqmail/notqmail/pull/1), [#20](https://github.com/notqmail/notqmail/pull/20), [#31](https://github.com/notqmail/notqmail/pull/31), [#53](https://github.com/notqmail/notqmail/pull/53), [#55](https://github.com/notqmail/notqmail/pull/55))

## Make packaging easier

- Fix builds on at least FreeBSD and macOS.
- Look up qmail's UIDs and GIDs at run time, not build time. ([#15](https://github.com/notqmail/notqmail/pull/15))
- Optionally install as non-root, to a staging area, with DESTDIR. ([#4](https://github.com/notqmail/notqmail/pull/4), [#15](https://github.com/notqmail/notqmail/pull/15))

## Other changes

- Add TravisCI config. ([#19](https://github.com/notqmail/notqmail/pull/19))
- Add `.gitignore`. ([#25](https://github.com/notqmail/notqmail/pull/25))
- Remove [precompiled var-qmail package](https://cr.yp.to/qmail/var-qmail.html) support. ([#15](https://github.com/notqmail/notqmail/pull/15))
- Remove `shar` target and `FILES`. ([#27](https://github.com/notqmail/notqmail/pull/27))
- Remove `SYSDEPS`. ([#33](https://github.com/notqmail/notqmail/pull/33))
- Replace `vfork()` with `fork()`, fixing macOS runtime. ([#38](https://github.com/notqmail/notqmail/pull/38))
- Update documents and URLs for notqmail. ([#39](https://github.com/notqmail/notqmail/pull/39), [#42](https://github.com/notqmail/notqmail/pull/42))

## GitHub references

- All [closed 1.07 issues](https://github.com/notqmail/notqmail/issues?q=is%3Aissue+is%3Aclosed+milestone%3A1.07)
- All [closed 1.07 PRs](https://github.com/notqmail/notqmail/pulls?q=is%3Apr+is%3Aclosed+milestone%3A1.07)


# How to install

## From source, on a single host

Fetch the [1.07 release in your preferred archive format](https://github.com/notqmail/notqmail/releases/tag/notqmail-1.07).

[Life with qmail](http://www.lifewithqmail.org/lwq.html#installation) continues to apply. Note that some modern systems — we've seen at least OpenBSD, FreeBSD, and Void Linux — don't provide `nroff`. [GNU troff](https://www.gnu.org/software/groff/) (aka `groff`) should do the trick. Also, please read our notes about [[patches]].

## From source, to many hosts

notqmail makes it easy to build once, install many.

### On the build host

Customize `conf-users` and `conf-groups`, if needed, and note the names. Then build, stage, and create a tarball:

    $ make it man
    $ export DESTDIR=/path/to/staging/directory
    $ make package
    $ tar -C ${DESTDIR} -czf notqmail-bin-1.07.tar.gz .

### On an install host

Copy over `notqmail-bin-1.07.tar.gz`, `instchown`, and `instcheck` from the build host. Extract the tarball -- e.g., with GNU Tar:

    # tar -C / --no-overwrite-dir -xzf notqmail-bin-1.07.tar.gz

[Create users and groups](https://github.com/notqmail/notqmail/blob/master/INSTALL.ids) with names to match the build. Set permissions on installed files:

    # ./instchown

Then verify the installation, just as with a traditional qmail install:

    # ./instcheck

## From vendor packages

Binary packages for many RPM and DEB based distributions are provided through [OpenBuildService](https://software.opensuse.org//download.html?project=home%3Anotqmail&package=notqmail).

### pkgsrc

    $ cd mail/qmail && make install

or on platforms with recent binary packages available,

    # pkg_add qmail


# Getting help

notqmail is discussed on the [qmail mailing list](https://cr.yp.to/lists.html#qmail) and on [Freenode's](https://freenode.net/) `#qmail` IRC channel.
For bug reports, please use our [issue tracker](https://github.com/notqmail/notqmail/issues) if possible.
For feature requests, please first refer to [Which features will eventually be implemented](https://github.com/notqmail/notqmail/wiki#which-features-will-eventually-be-implemented) and our [[roadmap]] for an idea of our current plans.
Then your rationale for how and why to change our plans -- which we are always open to -- will be more persuasive. :-)