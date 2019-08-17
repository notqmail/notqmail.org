You've been running qmail, so you've got a set of patches you rely on.
Your patches will mostly continue to apply to notqmail.
As notqmail gains features, you'll need fewer patches.

When one of your patches doesn't quite apply anymore, because notqmail's code has evolved out from under it, the patch needs to be "rebased" on top of notqmail.
Sometimes this is easy and mechanical.
Other times it will require deeper understanding of C, Unix, and qmail's design and implementation.
In both cases, Git can be a helpful tool.

For your convenience, we've prepared branches in the notqmail repo for several popular patches.
How to use:

1. Make sure the first commit on the branch is identical to the patch you're trying to apply.
2. Read the subsequent commits on the branch to see what we've changed and why.
3. Diff the branch against `master`, and apply _that_ as your patch to notqmail.

## notqmail patch branches

| Original Patch | Branch | Raw Diff |
| -------------- | ------ | -------- |
| [qmail-logmsg](http://free.acrconsulting.co.uk/email/qmail-logmsg.html) | [notqmail-smtpd-logging](https://github.com/notqmail/notqmail/compare/notqmail-smtpd-logging) | [notqmail-smtpd-logging.diff](https://github.com/notqmail/notqmail/compare/notqmail-smtpd-logging.diff)