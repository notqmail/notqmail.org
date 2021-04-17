You've been running qmail, so you've got a set of patches you rely on.
Your patches will mostly continue to apply to notqmail.
(See [#17](https://github.com/notqmail/notqmail/issues/17) for more about our intent.)
As notqmail gains features, you'll need fewer patches.

When one of your patches doesn't quite apply anymore, because notqmail's code has evolved out from under it, the patch needs to be "rebased".
Sometimes this is easy and mechanical.
Other times it will require deeper understanding of C, Unix, and qmail's design and implementation.
In both cases, Git can be a helpful tool.

For your convenience, we've rebased several popular patches onto notqmail, each on its own git branch.
How to use:

1. Make sure the first commit on the branch is identical to the patch you were trying to apply.
2. Read the subsequent commits on the branch to see what we've changed and why.
3. Diff the branch against `master`, and apply _that_ patch to notqmail.

## notqmail patch branches

| Branch | Original Patch |
| ------ | -------------- |
| [notqmail-badmailfrom-wildcard](https://github.com/notqmail/notqmail/commits/notqmail-badmailfrom-wildcard) | Tom Clegg's [badmailfrom wildcard](https://tomclegg.ca/qmail/#qmail-badmailfrom-wildcard) |
| [notqmail-badmailfrom-x-relayclient](https://github.com/notqmail/notqmail/commits/notqmail-badmailfrom-x-relayclient) | Jeremy Kitchen's [badmailfrom-x-relayclient](https://web.archive.org/web/20080907071938/http://scriptkitchen.com/qmail/badmailfrom-x-relayclient.patch)
| [notqmail-big-concurrency](https://github.com/notqmail/notqmail/commits/notqmail-big-concurrency) | Johannes Erdfelt's [big-concurrency](http://qmailorg.schmonz.com/big-concurrency.patch) |
| [notqmail-big-todo](https://github.com/notqmail/notqmail/commits/notqmail-big-todo) | Russell Nelson's [big-todo](http://qmailorg.schmonz.com/big-todo.103.patch)
| [master@b05ec6cbd](https://github.com/notqmail/notqmail/commit/b05ec6cbdacdf40d6c75326394461e22b7f8ab20) | Jonathan de Boyne Pollard's any-to-cname was integrated in [notqmail 1.08](https://github.com/notqmail/notqmail/releases/tag/notqmail-1.08) |
| [notqmail-dns-oversize](https://github.com/notqmail/notqmail/commits/notqmail-dns-oversize) | Christopher K. Davis's oversize DNS packet |
| [notqmail-ext-todo](https://github.com/notqmail/notqmail/commits/patches/notqmail/ext-todo) | André Opperman's ext_todo or "silly qmail syndrome" |
| [notqmail-smtp-auth](https://github.com/notqmail/notqmail/commits/patches/notqmail/smtp-auth) | Erwin Hoffmann's [smptauth](https://www.fehcom.de/qmail/smtpauth.html#PATCHES)
| [notqmail-smtp-tls](https://github.com/notqmail/notqmail/commits/patches/notqmail/smtp-tls) | Frederik Vermeulen's [qmail-smtp-tls](http://inoa.net/qmail-tls/)
| [notqmail-smtpd-logging](https://github.com/notqmail/notqmail/commits/notqmail-smtpd-logging) | Andrew Richards' [qmail-logmsg](http://free.acrconsulting.co.uk/email/qmail-logmsg.html) |
| [notqmail-smtpd-spf](https://github.com/notqmail/notqmail/commits/notqmail-smtpd-spf) | Jana Saout's [qmail-spf](https://www.saout.de/misc/spf/) |
 [qmail-spp-0.42](https://github.com/notqmail/notqmail/tree/patches/notqmail/qmail-spp-0.42) | [qmail spp](http://qmail-spp.sourceforge.net/) |
| [rcptcheck](https://github.com/notqmail/notqmail/tree/patches/notqmail/rcptcheck) | Jay Soffian's [rcptcheck](https://www.soffian.org/downloads/qmail/qmail-smtpd-doc.html) |
