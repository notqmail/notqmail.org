[[!meta title="Roadmap"]]

# 1.09.1

## Process improvements

### Website

- Discuss: historically remove many/most/all DJB-era `.md` docs from the source tree and preserve them on the website
    - Possibly false assumption: we were never going to update them
    - Possibly false assumption: they're not needed to grok/navigate the code
- Start a `next-release` page (excluding it from the [[releases]] feed)

### Git

- Redo patch branches (where needed) like so:
    1. Commit (if needed) to restore context we've changed
    2. Commit-with-attribution: upstream patch, as verbatim as possible
    3. Commit (if needed) to fix compilation, style, etc.

### Smoother PRs

- Focus for a while on automating sources of confidence:
    - Integrate [[!template id=pr number=225]] (the patch checker) into GitHub Actions
    - Make sure _automatically_ that `Makefile` rules listing dependencies on local include files are accurate
        - Also that `"foo.h"` includes come before `<foo.h>`
    - Automate noticing new versions of autobuilders
    - [[!template id=pr number=189]] Turn up warnings in local builds,
      fix everything that doesn't break patches, ratchet CI `conf-cc`
      `-Wthis -Wthat` to match
    - [[!template id=issue number=48]] Make regular use of code analysis tools
    - Reconsider alternatives to
      [check](https://libcheck.github.io/check),
      now that warnings are no longer rampant
        - For instance, [AceUnit](https://github.com/nelkinda/aceunit)
    - Write more tests
        - Integrated tests, too (such as [swaks](https://jetmore.org/john/code/swaks/))
- Discuss whether to keep maintaining an in-tree `CHANGES.md`
    - If yes, make PRs fail checks when we forget
    - Eike: let's keep `CHANGES.md` for changes that are user-facing, e.g.
        - autobuild workflow changes
        - information about _how_ we made it that isn't information about what's in there

### Smoother releases

- Make a small change, then cut another release, for the sole purpose of
  smoothing out the release process

# 1.10

## Cleanups

- [[!template id=issue number=7]] Stop redeclaring system functions
- Remove everything from 1.09 "What's going away?" that we're sure now is the time

## Patches to merge

- [[!template id=pr number=89]] Fix leap second handling on systems running TAI ([original patch](https://su.bze.ro/software/netqmail-1.05-TAI-leapsecs.patch))
- [[!template id=pr number=90]] Improve Maildir file uniqueness in qmail-local.c ([original patch](https://su.bze.ro/software/qmail-1.03-maildir-uniq.patch))
- [Sergio Gelato's fixed version of Andy Repton's outgoingip patch](https://qmail.notqmail.org/outgoingip.patch) to configure qmail-remote's IP in `control/outgoingip`
- [RCPTCHECK](http://www.soffian.org/downloads/qmail/qmail-smtpd-doc.html)
  or
  [qmail-spp](http://qmail-spp.sourceforge.net/doc/)
  (or both?)

## Ideas to merge

- [[!template id=issue number=94]] Sprinkle `fsync()` to make `syncdir` unnecessary
- Tiny changes to `qmail-smtpd` to support running under a `qmail-popup`-alike SMTP AUTH parent program

## Programs to merge

- [[!template id=pr number=227]] Import `qmail-qfilter`
    - [[!template id=pr number=232]] Test qmail-inject recipient address qualification
- [[!template id=pr number=233]] Import `qmail-rcptcheck`, `qmail-rcptcheck-realrcptto`, and `qmail-rcptcheck-badrcptto`
    - Enable `realrcptto` by default?
- Import [qmail-spp-spf](https://www.caputo.com/foss/qmail-spp-spf/)

## Other

- [[!template id=pr number=35]] FHS ([[!template id=issue number=2]])
  - split conf-qmail in to conf-qmail-bin, conf-qmail-queue, conf-qmail-man, etc.
  - `/var/qmail/DIR` unless `/var/qmail` not in `conf-qmail`
  - Configuration sugar: `./configure && make && make install` ([[!template id=issue number=9]])
- Debian (deb), RedHat (rpm), and /package packaging
  - [[!template id=pr number=76]] binary builds on openSUSE build service and locally
    - deb and rpm builds.  (was [[!template id=issue number=59]])
  - FHS-aware (default on): `/var/qmail` contains symlinks to FHS-compatible paths
  - FHS-strict (default off): `/var/qmail` does not exist
  - [[!template id=issue number=91]]

-----

# 1.11 and onward

- Incrementally integrate inbound STARTTLS and AUTH
- Incrementally redesign `qmail-remote` for outbound TLS, AUTH, SIZE, PIPELINING, SMTPUTF8, IPv6
- [[!template id=pr number=50]] Add `spawn-filter` for filtering messages from `qmail-remote` and `qmail-local`
- Add SRS and DKIM filters
- (see [[Designs]])

-----

# 1.19

## Publish some "extensions", if that still makes sense

- `qmail-popup`
- `qmail-pop3d`
- `qmail-qmtpd`
- `qmail-qmtpc`

-----

# 2.0

## Breaking changes to the queue

- new build time defaults for on-disk queue
- add queue repair tool
  - [[!template id=pr number=67]] remove qmail-upq
  - including the ability to upgrade a 1.x queue to 2.x in-place
- merge big-todo (changes queue layout)
- increase default conf-split to 31 (changes queue layout)
- merge ext-todo
  - add a qmail-todo manpage, [[!template id=issue number=23]]
- merge netqmail-big-concurrency

## Other breaking changes

- Merge changes for high-volume installations that are harmless defaults in 2020 (taking care to migrate smoothly)
- [qmail-ldap](http://www.nrg4u.com), or enough interfaces to let extensions provide LDAP integration
- make sure everything works with vmailmgr, vpopmail, other approaches to "virtual users"
- remove deprecated code
  - [[!template id=pr number=71]] remove install script

## Breaking changes to (some) patches

- [[!template id=pr number=43]] cleanup: remove `readwrite.h`, use `unistd.h` instead
- [[!template id=pr number=44]] cleanup: remove `exit.h`, use `unistd.h` instead
- cleanup: remove `fork.h`, use `unistd.h` instead

Port to the latest DJB libraries.
Remove local copies.
Depend on external libowfat or skalibs.

- Replace [stralloc](https://cr.yp.to/lib/stralloc.html) with [array](https://cr.yp.to/lib/array.html)
- Replace substdio with [buf](https://cr.yp.to/lib/buffer_get.html)[fer](https://cr.yp.to/lib/buffer_put.html)
- Replace time-handling code with [libtai](https://cr.yp.to/libtai/tai.html)
- Replace DNS resolver code with [djbdns's](https://cr.yp.to/djbdns/dns.html)
- [[!template id=issue number=88]] Use [mess822](https://cr.yp.to/mess822.html)
- Replace poll/select with [iopause](https://cr.yp.to/lib/iopause.html)
  - Possibly add kqueue and/or epoll support to iopause
- Replace exec (and related env_puts) with [pathexec](https://cr.yp.to/lib/pathexec.html)
- Update to latest [cdb](https://cr.yp.to/cdb/reading.html)
- Use [socket](https://cr.yp.to/lib/socket.html) for any remaining networking code that's still necessary


-----

# 2.1

## Port unmerged, blessed netqmail patches to the extension interface

-----

# 2.2

## Extensions for postmaster interfaces

- Help developers adapt some code of theirs and get it merged

-----

# 2.3

## Extensions for email clients

- Help developers convert more of their existing code to extensions
