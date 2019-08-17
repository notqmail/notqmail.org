You've been running qmail, so you've got a set of patches you rely on.
Your patches will mostly continue to apply to notqmail.
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

| Original Patch | Branch | Raw Diff |
| -------------- | ------ | -------- |
| [qmail-logmsg](http://free.acrconsulting.co.uk/email/qmail-logmsg.html) | [notqmail-smtpd-logging](https://github.com/notqmail/notqmail/compare/notqmail-smtpd-logging) | [notqmail-smtpd-logging.diff](https://github.com/notqmail/notqmail/compare/notqmail-smtpd-logging.diff) |
| [qmail-badmailfrom-wildcard](https://tomclegg.ca/qmail/#qmail-badmailfrom-wildcard) | [netqmail-badmailfrom-wildcard](https://github.com/notqmail/notqmail/compare/netqmail-badmailfrom-wildcard) | [netqmail-badmailfrom-wildcard.diff](https://github.com/notqmail/notqmail/compare/netqmail-badmailfrom-wildcard.diff) |
| [badmailfrom-x-relayclient](https://web.archive.org/web/20080907071938/http://scriptkitchen.com/qmail/badmailfrom-x-relayclient.patch) | [netqmail-badmailfrom-x-relayclient](https://github.com/notqmail/notqmail/compare/netqmail-badmailfrom-x-relayclient) | [netqmail-badmailfrom-x-relayclient.diff](https://github.com/notqmail/notqmail/compare/netqmail-badmailfrom-x-relayclient.diff) |
| [big-concurrency](http://qmailorg.schmonz.com/big-concurrency.patch) | [netqmail-big-concurrency](https://github.com/notqmail/notqmail/compare/netqmail-big-concurrency) | [netqmail-big-concurrency.diff](https://github.com/notqmail/notqmail/compare/netqmail-big-concurrency.diff) |
| [big-todo](http://qmailorg.schmonz.com/big-todo.103.patch) | [netqmail-big-todo](https://github.com/notqmail/notqmail/compare/netqmail-big-todo) | [netqmail-big-todo.diff](https://github.com/notqmail/notqmail/compare/netqmail-big-todo.diff) |