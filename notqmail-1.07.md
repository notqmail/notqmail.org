_---It's not [qmail](https://cr.yp.to/qmail.html). It's also not [netqmail](http://netqmail.org).---_

notqmail, a Unix mail transfer agent (MTA), is a fork of qmail in the netqmail family.  notqmail is a community-assembled distribution to provide an extensible, packaged qmail.  Our goal is to provide stable, compatible, regular releases that will not break or conflict with your local site customization.

**NOTE:** This release is under development and not yet published.

## What's New

notqmail-1.07 supports staged installation, where build and packaging is done on one host for installation to another.  notqmail can be built and packaged without requiring qmail system accounts or on a build hosts where the uid/gid values for those accounts differ from the install host.

notqmail-1.07 now builds on FreeBSD and Mac OS X.

* Staged installation
    * the setup target supports the DESTDIR environment variable for staged installation outside of `/var/qmail`.
    * a new target, package, will make a staged qmail install as a regular (non-root) user.
    * The program instchown is run on the install host to set file ownership and other root-required installation steps.
    * uid/gid lookup of qmail system accounts is now done at runtime.  
* Build platforms
    * FreeBSD: build on utmpx-only systems.
    * Mac OS X: build on case-insensitive filesystems, enable compatibility mode for name resolution, work around linker error.
* Correctness and cleanup
    * Add missing function arguments, Makefile dependencies, and missing header files.
    * Remove precompiled var qmail package support.

## How to install

The instructions for building and installing notqmail on a single host are unchanged.  This release introduces the option to perform a staged install, allowing notqmail to be built and packaged on one machine and run on another.

On the build host:

    make it man
    DESTDIR=/path/to/staging/directory make package
    # create a tar archive of the staging directory and instchown.


On the install host:

    # untar the contents of the staging directory in to conf-qmail.
    # create qmail system accounts.
    ./instchown