[[!meta title="About"]]


# What is notqmail?

_It's not qmail. It's also not netqmail._

We all use email, so we all use email servers. notqmail is software for running an [email server](https://en.wikipedia.org/wiki/Message_transfer_agent). Someday, if we do a good job, some of the many [articles about how and why to run your own](https://arstechnica.com/information-technology/2014/02/how-to-run-your-own-e-mail-server-with-your-own-domain-part-1/) will recommend notqmail.


## Why not Postfix?

[Postfix](http://www.postfix.org) is very good. We also really like qmail.

For now, we're targeting sysadmins who already run a qmail-based mail system. If it's not clear to you why you'd run notqmail instead of Postfix, you're probably right. Someday, when notqmail is more featureful, we'll want to compare and contrast with other MTAs. In the meantime, many of [qmail 1.03's advantages](https://cr.yp.to/qmail.html) are still relevant.


## Why should I trust notqmail?

This is a big question and it deserves a [[thorough answer|Trust]].


## Are DJB or any of the netqmail authors involved?

Neither netqmail nor DJB were asked to approve of this distribution.


## Does the [qmail security guarantee](https://cr.yp.to/qmail/guarantee.html) apply?

Sorry, no. We're not DJB, and notqmail is not qmail.


## What are the project's goals?

See:

- [[Goals and Non-Goals|goals-and-non-goals]]
- [[Feature Wishlist|feature-wishlist]]
- [[Designs]]
- [[Roadmap]]


## What happens to my custom patchset?

Expect your patchset to:

- Mostly continue to apply
- Gradually shrink as new notqmail releases include more of the features and bugfixes you need
- Eventually shrink to zero, if your needs are widely shared by others

For more, see [[Patches]].


## How do I install notqmail?

Your build scripts will continue to work.
We've tested many [[platforms]].
See [[Install]].


## How can I get more involved?

Our [git repository](https://github.com/notqmail/notqmail) and [issue tracker](https://github.com/notqmail/notqmail/issues) are hosted by GitHub.  Various contributors to notqmail are active on the [qmail mailing list](https://cr.yp.to/lists.html#qmail) and on [Libera Chat's](https://libera.chat/) `#qmail` IRC channel.

We invite users or enthusiasts of qmail to join us. We especially hope for:

- Ideas and feedback from those of you running (or not quite running) qmail
- Code from those of you with custom patchsets or forks

Say hi on the list or IRC and one of us will help you get started on your first contribution.
