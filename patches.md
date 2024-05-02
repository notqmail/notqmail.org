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

Please note that the patch branches are likely to be _re_-rebased from time to time (for instance, around notqmail release time).
Take care when fetching these git branches, especially if you have local changes you need to preserve.

## notqmail patch branches

[[!table data="""
Branch | Original Patch
[[!template id=patch name=badmailfrom-wildcard]] | Tom Clegg's [badmailfrom wildcard](https://tomclegg.ca/qmail/#qmail-badmailfrom-wildcard)
[[!template id=patch name=badmailfrom-x-relayclient]] | Jeremy Kitchen's [badmailfrom-x-relayclient](https://web.archive.org/web/20080907071938/http://scriptkitchen.com/qmail/badmailfrom-x-relayclient.patch)
[[!template id=patch name=big-concurrency]] | Johannes Erdfelt's [big-concurrency](https://qmail.notqmail.org/big-concurrency.patch)
[[!template id=patch name=big-todo]] | Russell Nelson's [big-todo](https://qmail.notqmail.org/big-todo.103.patch)
[[!template id=patch name=ext-todo]] | Claudio Jeker's and André Oppermann's [ext-todo](http://www.nrg4u.com/qmail/ext_todo-20030105.patch) (for "silly qmail syndrome")
[[!template id=patch name=smtp-auth]] | Erwin Hoffmann's [smtpauth](https://www.fehcom.de/qmail/smtpauth.html##PATCHES)
[[!template id=patch name=smtp-tls]] | Frederik Vermeulen's [qmail-smtp-tls](https://inoa.net/qmail-tls/)
[[!template id=patch name=smtpd-logging]] | Andrew Richards' [qmail-logmsg](https://free.acrconsulting.co.uk/email/qmail-logmsg.html)
[[!template id=patch name=smtpd-spf]] | Jana Saout's [qmail-spf](https://www.saout.de/misc/spf/)
[[!template id=patch name=smtpd-spp]] | Paweł Foremski's [qmail-spp](https://qmail-spp.sourceforge.net/)
[[!template id=patch name=rcptcheck]] | Jay Soffian's [rcptcheck](https://www.soffian.org/downloads/qmail/qmail-smtpd-doc.html)
"""]]
