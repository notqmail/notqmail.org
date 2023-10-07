[[!meta title="Doing Releases"]]

This is my cheatsheet about what I have been doing to get the notqmail-1.08 release out of the door.

## Pre-release checks

Make sure the expected popular patches (TLS, ...) still apply, or that we've prepared rebased versions that do.

## Wiki page

We collected all merged PRs on the wiki paged named like the release.

## Release tag

The tag was done using

```shell
git tag -s notqmail-1.08
```

The first line of the tag description is the release name without the dash, i.e. ```notqmail 1.08```.

The rest of that description are the bullet points from the wiki page. It does not include the intermediate headlines and other comments.

## Tarballs

```shell
RELEASE=1.08
git archive --prefix=notqmail-${RELEASE}/ -o notqmail-${RELEASE}.tar notqmail-${RELEASE}
gzip --best --keep notqmail-${RELEASE}.tar
xz --best notqmail-${RELEASE}.tar
gpg --detach-sign -a -o notqmail-${RELEASE}.tar.xz.sig notqmail-${RELEASE}.tar.xz
gpg --detach-sign -a -o notqmail-${RELEASE}.tar.gz.sig notqmail-${RELEASE}.tar.gz
```

## GitHub release page

Use the tag, copy all the text, click edit release, paste the text. Add spaces around the dashes at the beginning of each line so that they will show up as real bullet points when shown. Upload the 4 files (2 tarballs, 2 signatures). Publish release.
