[[!meta title="Patches"]]

## Everyone has patches

You've been running qmail, so you've got a local set of patches you rely on.
Your patches will mostly continue to apply to notqmail.
(See [[!template id=issue number=17]] for more about our intent.)
As notqmail gains features, you'll need fewer patches.

## notqmail might break patches by mistake

If your local patches apply, but compiling fails, it might be due to a deprecated function.
Add `-DDEPRECATED_FUNCTIONS_AVAILABLE` to `conf-cc` and try again.
If this makes your build succeed, we need to know!
Please [file an issue](https://github.com/notqmail/notqmail/issues/new/choose) with the build error you had seen and the patch(es) involved.

## Everyone maintains patches

When qmail stopped being updated, your patches stopped needing updating.
As notqmail's code evolves, your local patches may need to be "rebased".
Sometimes this is easy and mechanical.
Other times it will require deeper understanding of C, Unix, and qmail's design and implementation.
In either case, Git can be a helpful tool.

For your convenience, we've rebased several popular patches onto notqmail, each on its own git branch.
How to use:

1. Make sure the first commit on the branch is identical to the patch you were trying to apply.
2. Read the subsequent commits on the branch to see what we've changed and why.
3. Diff the branch against `master`, and apply _that_ patch to notqmail.

## notqmail patch branches

[[!table data="""
Branch | Original Patch
[notqmail-badmailfrom-wildcard](https://github.com/notqmail/notqmail/commits/notqmail-badmailfrom-wildcard) | Tom Clegg's [badmailfrom wildcard](https://tomclegg.ca/qmail/#qmail-badmailfrom-wildcard)
[notqmail-badmailfrom-x-relayclient](https://github.com/notqmail/notqmail/commits/notqmail-badmailfrom-x-relayclient) | Jeremy Kitchen's [badmailfrom-x-relayclient](https://web.archive.org/web/20080907071938/http://scriptkitchen.com/qmail/badmailfrom-x-relayclient.patch)
[notqmail-big-concurrency](https://github.com/notqmail/notqmail/commits/notqmail-big-concurrency) | Johannes Erdfelt's [big-concurrency](https://qmail.notqmail.org/big-concurrency.patch)
[notqmail-big-todo](https://github.com/notqmail/notqmail/commits/notqmail-big-todo) | Russell Nelson's [big-todo](https://qmail.notqmail.org/big-todo.103.patch)
[notqmail-dns-oversize](https://github.com/notqmail/notqmail/commits/notqmail-dns-oversize) | Christopher K. Davis's oversize DNS packet
[notqmail-ext-todo](https://github.com/notqmail/notqmail/commits/patches/notqmail/ext-todo) | André Opperman's ext_todo or "silly qmail syndrome"
[notqmail-smtp-auth](https://github.com/notqmail/notqmail/commits/patches/notqmail/smtp-auth) | Erwin Hoffmann's [smtpauth](https://www.fehcom.de/qmail/smtpauth.html##PATCHES)
[notqmail-smtp-tls](https://github.com/notqmail/notqmail/commits/patches/notqmail/smtp-tls) | Frederik Vermeulen's [qmail-smtp-tls](http://inoa.net/qmail-tls/)
[notqmail-smtpd-logging](https://github.com/notqmail/notqmail/commits/notqmail-smtpd-logging) | Andrew Richards' [qmail-logmsg](http://free.acrconsulting.co.uk/email/qmail-logmsg.html)
[notqmail-smtpd-spf](https://github.com/notqmail/notqmail/commits/notqmail-smtpd-spf) | Jana Saout's [qmail-spf](https://www.saout.de/misc/spf/)
[qmail-spp-0.42](https://github.com/notqmail/notqmail/tree/patches/notqmail/qmail-spp-0.42) | [qmail spp](http://qmail-spp.sourceforge.net/)
[rcptcheck](https://github.com/notqmail/notqmail/tree/patches/notqmail/rcptcheck) | Jay Soffian's [rcptcheck](https://www.soffian.org/downloads/qmail/qmail-smtpd-doc.html)
"""]]
