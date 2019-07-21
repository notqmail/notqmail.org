notqmail is a fork of netqmail-1.06.  Prior releases of netqmail and qmail are available to branch from, with additional branches for published, noteworthy patches to netqmail-1.06.

The notqmail release roadmap:

# [[1.07|notqmail-1.07]]
## Fix broken builds
- FreeBSD
- Mac OS X
## Make packaging easier
- Stage installation into `${DESTDIR}`
- Look up UIDs and GIDs at runtime (and build without requiring qmail system accounts as a regular, non-`root` user)

# 1.08
## Debian (deb) and RedHat (rpm) packaging
- FHS-aware (default on): `/var/qmail` contains symlinks to FHS-compatible paths
- FHS-strict (default off): `/var/qmail` does not exist
- Configuration sugar: `./configure && make && make install`
- Add package builds to tree.
## Fix incorrect behavior
- Link with [syncdir](http://untroubled.org/syncdir/)
- [TAI system clock](https://su.bze.ro/software/netqmail-1.05-TAI-leapsecs.patch)
- [Revised Maildir protocol](https://su.bze.ro/software/qmail-1.03-maildir-uniq.patch)
- [Big DNS](https://www.ckdhr.com/ckd/qmail-103.patch)
- [qmail-remote: avoid recoding CRLF to CRCRLF](https://github.com/notqmail/notqmail/pull/18)
- Delete obsolete qmail binaries (`idedit`, `install-big`, ...).
- Refactor the C code, by replacing valid K&R (The C Programming Language first edition) constructs with valid C89 (ANSI, The C Programming Language second edition) constructs, when there is a C89 feature that supersedes a construct in K&R.  (e.g., function signatures, adding int type specifiers.)  Even when a K&R construct is legal in C89.
- Fix all compiler warnings generated by warning settings consistent with the codebase being legal C89, and possibly informed by later C standards, to include at least the default `conf-cc`.

# 1.9
## Introduce new programming interfaces for use by extensions
- No functional changes intended
- [Specify an alternate qmail-remote](https://schmonz.com/qmail/remote/netqmail-1.06-qmailremote-20170716.patch) (just like QMAILQUEUE)
- [Custom error strings for qmail-queue](https://notes.sagredo.eu/files/qmail/patches/qmail-queue-custom-error-v2.netqmail-1.05.patch)
- [Extension API for qmail-smtpd](http://qmail-spp.sourceforge.net)
- publish qmail-qmtpd and qmail-qmtpc as extensions.

# 2.0
## queue-breaker release
- new build time defaults for on-disk queue
- add queue repair tool.
-- including the ability to upgrade a 1.x queue to 2.x in-place.
- merge big-todo (changes queue layout)
- increase default conf-split to 31 (changes queue layout)
- merge ext-todo
- merge netqmail-big-concurrency
- Merge changes for high-volume installations that are harmless defaults in 2019 (taking care to migrate smoothly)

# 2.1
## Port unmerged, blessed netqmail patches to the extension interface

# 2.2
## Extensions for postmaster interfaces
- Help developers adapt some code of theirs and get it merged

# 2.3
## Extensions for email clients
- Help developers convert more of their existing code to plugins