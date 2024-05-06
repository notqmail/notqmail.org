[[!meta title="Doing Releases"]]

## Prerequisites

### A week(ish) before

- Validate autobuilds: green recently? updated with all `-Werror` classes that we've eradicated recently?
- Stop merging things
- Create a draft "pre-release" "Save draft"
  [via GitHub's release GUI](https://github.com/notqmail/notqmail/releases/new),
  converting ikiwiki release notes to GitHub via the `html2text` pipeline below
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

## 1. Submit a version-bump PR

Ensure release notes and `CHANGES.md` are in sync (if we're still using both), then:

[[!format sh """
vi Makefile	# bump RELEASE_VERSION
make release-changes release-copyright
git diff
make release-commit
"""]]

## 2. Have the version-bump PR merged

Requires 2 reviewers (as any PR).

## 3. Create the release tag

Don't use GitHub's release notes GUI for this (can't PGP-sign tags).
Instead:

[[!format sh """
make release-tag
make release-tag-push
"""]]

The first line of the tag description is the release name without the dash, i.e. "notqmail 1.09".
The rest of it is a reduced version of the release notes:
just the bullet points, no intermediate headlines or other comments.

## 4. Trivially re-rebase our patch branches

Don't automate this, but do walk the list like so:

[[!format sh """
for i in $(git branch -r | grep origin/patches/notqmail/ | sed -e 's|origin/||'); do
    git checkout $i
    git rebase master
    git push -f origin HEAD
done
"""]]

## 5. Create the release

[[!format sh """
make release-tarballs
make release-signatures
"""]]

Copy the website's release notes to clipboard in GitHub format one last time:

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

From the
[release notes GUI](https://github.com/notqmail/notqmail/releases):

1. Find the draft release already in progress.
2. Edit it.
3. At top, for "Choose a tag", choose the newly created tag.
4. At bottom, for "Attach binaries", upload the 4 artifacts (2 tarballs, 2 sigs).
5. At center, for the release notes, select-all and paste
6. At bottom, set as the latest release, and publish!

## 6. Push release notes to the website

Merge the local (or prod) branch to `main`.

Maybe also push copies of the release artifacts?

## 7. Post everywhere about the new release

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

## 8. Update packages we control

1. [Open Build Service](https://build.opensuse.org/package/show/home:notqmail/notqmail)
    - RPM builds: `notqmail.spec` (bump version number)
    - Debian builds: `notqmail.dsc` (bump version number)
    - for the `.tar.gz` link: `_service` (update tarball link)
2. [Gentoo](https://gitweb.gentoo.org/repo/gentoo.git/tree/mail-mta/notqmail) (`DerDakon`)
3. [pkgsrc](https://github.com/NetBSD/pkgsrc/tree/trunk/mail/qmail) (`schmonz`)

## 9. Review and adjust the [[roadmap]]

- Remember where we thought we wanted to go from here
- Add/change/defer/remove as needed
