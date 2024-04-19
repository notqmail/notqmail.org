[[!meta title="Patches"]]

## Everyone has patches

You've been running qmail, so you've got a local set of patches you rely on.
In the years when qmail wasn't being updated, your patches easily applied (and re-applied) to a non-moving target.
As notqmail's code evolves, some of your patches will no longer be needed, and others may need to be "rebased" to apply.
(Sometimes this is easy and mechanical.
Other times it will require deeper understanding of C, Unix, and qmail's design and implementation.
In either case, Git can be a helpful tool.)

On balance, over time, we intend to reduce your patch-related maintenance effort.
For more about our intent, see
[[!template id=issue number=17]].

## Check our work

Once your patched notqmail is happily compiling, please help it stay
that way: add `-DDEPRECATED_FUNCTIONS_REMOVED` to `conf-cc` and
[report an issue](https://github.com/notqmail/notqmail/issues/new/choose)
if the build now fails.
Otherwise, we may unknowingly remove functions your patches are relying on in an upcoming release.

## Let us help

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
[notqmail-ext-todo](https://github.com/notqmail/notqmail/commits/patches/notqmail/ext-todo) | Claudio Jeker's and André Oppermann's ext_todo or "silly qmail syndrome"
[notqmail-smtp-auth](https://github.com/notqmail/notqmail/commits/patches/notqmail/smtp-auth) | Erwin Hoffmann's [smtpauth](https://www.fehcom.de/qmail/smtpauth.html##PATCHES)
[notqmail-smtp-tls](https://github.com/notqmail/notqmail/commits/patches/notqmail/smtp-tls) | Frederik Vermeulen's [qmail-smtp-tls](http://inoa.net/qmail-tls/)
[notqmail-smtpd-logging](https://github.com/notqmail/notqmail/commits/notqmail-smtpd-logging) | Andrew Richards' [qmail-logmsg](http://free.acrconsulting.co.uk/email/qmail-logmsg.html)
[notqmail-smtpd-spf](https://github.com/notqmail/notqmail/commits/notqmail-smtpd-spf) | Jana Saout's [qmail-spf](https://www.saout.de/misc/spf/)
[qmail-spp-0.42](https://github.com/notqmail/notqmail/tree/patches/notqmail/qmail-spp-0.42) | [qmail spp](http://qmail-spp.sourceforge.net/)
[rcptcheck](https://github.com/notqmail/notqmail/tree/patches/notqmail/rcptcheck) | Jay Soffian's [rcptcheck](https://www.soffian.org/downloads/qmail/qmail-smtpd-doc.html)
"""]]
