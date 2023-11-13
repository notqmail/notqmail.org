[[!meta title="Install"]]

## From source, on a single host

Fetch [the latest release](https://github.com/notqmail/notqmail/releases) in your preferred archive format.

[Life with qmail](http://www.lifewithqmail.org/lwq.html#installation) continues to apply. Note that some modern systems -- we've seen at least OpenBSD, FreeBSD, and Void Linux -- don't provide `nroff`. [GNU troff](https://www.gnu.org/software/groff/) (aka `groff`) should do the trick. Also, please read our notes about [[patches]].

## From source, to many hosts

notqmail makes it easy to build once, install many.

### On the build host

Customize `conf-users` and `conf-groups`, if needed, and note the names. Then build, stage, and create a tarball:

    $ make it man
    $ export DESTDIR=/path/to/staging/directory
    $ make package
    $ tar -C ${DESTDIR} -czf notqmail-bin-VERSION.tar.gz .

### On an install host

Copy over `notqmail-bin-VERSION.tar.gz`, `instchown`, and `instcheck` from the build host. Extract the tarball -- e.g., with GNU Tar:

    # tar -C / --no-overwrite-dir -xzf notqmail-bin-VERSION.tar.gz

[Create users and groups](https://github.com/notqmail/notqmail/blob/master/INSTALL.ids.md) with names to match the build. Set permissions on installed files:

    # ./instchown

Then verify the installation, just as with a traditional qmail install:

    # ./instcheck

## From vendor packages

Binary packages for many RPM and DEB based distributions are provided through [OpenBuildService](https://software.opensuse.org//download.html?project=home%3Anotqmail&package=notqmail).

### pkgsrc

    $ cd mail/qmail && make install

or on platforms with recent binary packages available,

    # pkg_add qmail

