We've imported qmail and netqmail into git, with tags at each historical version. Our starting point for notqmail is netqmail 1.06.

Our current intentions, which we'll update periodically as we get better ideas, are:

# 1.07
## Fix broken builds
- FreeBSD
- Mac OS X
## Make packaging easier
- Stage installation into `${DESTDIR}`
- Look up UIDs and GIDs at runtime (and build as non-`root`)
- FHS-aware (default on): `/var/qmail` contains symlinks to FHS-compatible paths
- FHS-strict (default off): `/var/qmail` does not exist
- Configuration sugar: `./configure && make && make install`
- Delete unused qmail code (`idedit`, `install-big`...)

# 1.08
## Fix incorrect behavior
- Link with [syncdir](http://untroubled.org/syncdir/)
- [TAI system clock](https://su.bze.ro/software/netqmail-1.05-TAI-leapsecs.patch)
- [Revised Maildir protocol](https://su.bze.ro/software/qmail-1.03-maildir-uniq.patch)
- [Big DNS](https://www.ckdhr.com/ckd/qmail-103.patch)
- [qmail-remote: avoid recoding CRLF to CRCRLF](https://github.com/notqmail/notqmail/pull/18)

# 1.09
## Introduce new programming interfaces for use by "plugins"
- No functional changes intended
- [Specify an alternate qmail-remote](https://schmonz.com/qmail/remote/netqmail-1.06-qmailremote-20170716.patch) (just like QMAILQUEUE)
- [Custom error strings for qmail-queue](https://notes.sagredo.eu/files/qmail/patches/qmail-queue-custom-error-v2.netqmail-1.05.patch)
- [Plugin API for qmail-smtpd](http://qmail-spp.sourceforge.net)

# 1.10
## Add some plugins
- Help developers adapt some code of theirs and get it merged

# 1.11
## Add more plugins
- Help developers convert more of their existing code to plugins

# 2.0
## queue-breaker release
- add queue repair tool.
-- including the ability to upgrade a 1.x queue to 2.x in-place.
- merge big-todo (changes queue layout)
- merge ext-todo
- merge netqmail-big-concurrency
- Merge changes for high-volume installations that are harmless defaults in 2019 (taking care to migrate smoothly)

# 2.1
## code modernization and ...
- Freely and invasively modernize to C99
- Freely and invasively fix all compiler warnings

# Maybe later
- Merge multiple implementations of a feature into one "blessed" plugin
- Delete unused plugins
