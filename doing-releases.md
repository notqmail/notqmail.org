[[!meta title="Doing Releases"]]

## Prerequisites

### A week(ish) before

- Validate autobuilds: green recently?
- Stop merging things
- Prepare and review release notes
- File an issue for results of patch testing (and rebasing)
- Manually test that popular [[patches]] apply and build, and perhaps
  even that their runtime behavior looks right

### During

- 3 people
    - 1 with a working PGP key and passphrase and a clean `git` checkout
    - 2 reviewers so release PRs can be merged immediately
      (currently
      [these people](https://github.com/orgs/notqmail/people))
- 15 minutes for the autobuilds to run green

### Shortly after

- 1 person with access to
  [Open Build Service](https://build.opensuse.org/project/show/home:notqmail)
  (currently
  [these people](https://build.opensuse.org/project/users/home:notqmail))

-----

## 1. Submit a PR for the version-bump changes

- Sync release notes with `CHANGES.md`
	- If we are still trying to manage change entries in two places
- Bump `RELEASE_VERSION` in `Makefile, then:
    - `make release-changes release-copyright`
    - `git diff`
    - `make release-commit`
- `COPYRIGHT` with an updated claim (or lack thereof)
- Add any new specific `-Werror` classes of warning that we've eradicated to all the autobuilds, if we haven't done so already (better to do it at the time)

## 2. Have the version-bump PR merged

- Requires 2 reviewers (as any PR)

## 3. Create the release tag

- Not from the release notes GUI, from the command line (in order to PGP-sign)

[[!format sh """
git tag -s notqmail-1.09
"""]]

The first line of the tag description is the release name without the dash, i.e. `notqmail 1.09`.

The rest of that description are the bullet points from the wiki page. It does not include the intermediate headlines and other comments.

## 4. Trivially re-rebase our patch branches

- On top of the new tag

## 5. Put release notes in GitHub

[here](https://github.com/notqmail/notqmail/releases/new)

Choose the already created tag.
Copy release notes from locally staged website:

[[!format sh """
cat html/releases/1.09/index.html \
| sed -e 's| href="\.\.\/\.\.\/| href="https://notqmail.org/|g' \
    -e 's| href="\.\./| href="https://notqmail.org/releases/|g' \
| html2text --body-width 0 \
| sed -e '1d' \
| grep -v '^Last edited ' \
| grep -v '^Mirror: ' \
| pbcopy
"""]]

Paste the release notes.
Upload the 4 files (2 tarballs, 2 signatures).
Publish release.

## 6. Create, PGP-sign, and upload tarballs to GitHub

[[!format sh """
RELEASE=1.08
git archive --prefix=notqmail-${RELEASE}/ -o notqmail-${RELEASE}.tar notqmail-${RELEASE}
gzip --best --keep notqmail-${RELEASE}.tar
xz --best notqmail-${RELEASE}.tar
gpg --detach-sign -a -o notqmail-${RELEASE}.tar.xz.sig notqmail-${RELEASE}.tar.xz
gpg --detach-sign -a -o notqmail-${RELEASE}.tar.gz.sig notqmail-${RELEASE}.tar.gz
"""]]

Web-upload them [here again](https://github.com/notqmail/notqmail/releases)

Maybe self-host copies of the release tarballs?

## 7. Push release notes to the website

Merge the local (or prod) branch to `main`.

## 8. Update packages we control

1. [Open Build Service](https://build.opensuse.org/package/show/home:notqmail/notqmail)
    - RPM builds: `notqmail.spec` (bump version number)
    - Debian builds: `notqmail.dsc` (bump version number)
    - for the `.tar.gz` link: `_service` (update tarball link)
2. [Gentoo](https://gitweb.gentoo.org/repo/gentoo.git/tree/mail-mta/notqmail) (`DerDakon`)
3. [pkgsrc](https://github.com/NetBSD/pkgsrc/tree/trunk/mail/qmail) (`schmonz`)

## 9. Post everywhere about the new release

1. Mailing lists:
    - the qmail list
    - maybe a new `users@` list at notqmail.org?
2. Discussion forums:
    - [Lobste.rs](https://lobste.rs/stories/new)
    - [Hacker News](https://news.ycombinator.com/submit)
    - [Slashdot](https://slashdot.org/submission)
    - [LWN](https://lwn.net/Articles/796794/)
    - [UnitedBSD](https://www.unitedbsd.com/d/863-bsd-news-thread/138)
    - [Phoronix](https://www.phoronix.com/)
3. Social media
    - [Twitter @notqmail](https://twitter.com/notqmail)
    - [Fediverse @notqmail](https://social.notqmail.org/notqmail)

## 10. Review and adjust the [[roadmap]]

- Remember where we thought we wanted to go from here
- Add/change/defer/remove as needed
