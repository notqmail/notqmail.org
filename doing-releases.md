[[!meta title="Doing Releases"]]

## Prerequisites

- 3 people (because 2 reviewers)
- Someone with access to the Open Build Service package
	- currently `mbhangui` and `DerDakon`
	- any of us can/should request access
- A release engineer with a working PGP key and passphrase
- A clean, up-to-date `git` working tree
- Team willingness to stop merging changes for hours to days (maximum 1 week)
    - so we can test the expected popular [[patches]] (TLS, ...) and rebase any that need it
- A few days before, make a branch with a trivial fake change that won't break anything, to force all CI builds, to make sure they build!
- At release time, some hours -- to wait for all the CI builds, which can take arbitrarily long

## After 1.09

- Start a `notqmail.org` page for `next-release`, excluding it from the releases RSS feed
- Amitai should stop having `origin` be his fork
- Let's make a small change, then cut another release (1.09.1?),
  in order to practice and smooth out the release process

## 1. Draft release notes in advance

(on a local ikiwiki instance, or maybe on a branch of the prod site)

## 2. Submit a PR for the version-bump changes

- Sync release notes with `CHANGES.md`
	- If we are still trying to manage change entries in two places
- Add new version to `CHANGES.md`, e.g. using this `gmake(1)` syntax:
    - `sed -i "1i - $(shell date +%Y%m%d) version: notqmail $(RELEASE_VERSION)" CHANGES.md`
    - `git commit -S -m "notqmail $(RELEASE_VERSION)" CHANGES.md`
	- etc. (this will be automated in `Makefile` by Dakon)
- `COPYRIGHT` with an updated claim (or lack thereof)
- Add any new specific `-Werror` classes of warning that we've eradicated to all the autobuilds, if we haven't done so already (better to do it at the time)

## 3. Have the version-bump PR merged

- Requires 2 reviewers (as any PR)

## 4. Create the release tag

- Not from the release notes GUI, from the command line (in order to PGP-sign)

[[!format sh """
git tag -s notqmail-1.09
"""]]

The first line of the tag description is the release name without the dash, i.e. `notqmail 1.09`.

The rest of that description are the bullet points from the wiki page. It does not include the intermediate headlines and other comments.

## 5. Trivially re-rebase our patch branches

- On top of the new tag

## 6. Put release notes in GitHub

[here](https://github.com/notqmail/notqmail/releases/new)

Use the tag, copy all the text, click edit release, paste the text. Add spaces around the dashes at the beginning of each line so that they will show up as real bullet points when shown. Upload the 4 files (2 tarballs, 2 signatures). Publish release.

("paste the text" needs to be Markdown that GitHub can parse -- so commit release notes to ikiwiki, then convert the generated HTML to Markdown, such as with `html2text`. Also make sure lines are not hard-wrapped, make sure they're long)

## 7. Create, PGP-sign, and upload tarballs to GitHub

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

## 8. Push release notes to the website

Merge the local (or prod) branch to `main`.

## 9. Update Open Build Service

- RPM builds: `notqmail.spec` (bump version number)
- Debian builds: `notqmail.dsc` (bump version number)
- for the `.tar.gz` link: `_service` (update tarball link)
- Where to do it: <https://build.opensuse.org/package/show/home:notqmail/notqmail>

## 10. Update Gentoo (`DerDakon`)

## 11. Update pkgsrc (`schmonz`)

## 12. Post everywhere about the new release

- qmail mailing list
- Lobste.rs
- Social media (`schmonz` does this a lot anyway)
	- Need a "notqmail" Mastodon account
- Hacker News
- Slashdot
