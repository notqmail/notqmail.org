# What is notqmail?

_It's not qmail. It's also not netqmail._

We all use email, so we all use email servers. notqmail is software for running an [email server](https://en.wikipedia.org/wiki/Message_transfer_agent). Someday, if we do a good job, some of the many [articles about how and why to run your own](https://arstechnica.com/information-technology/2014/02/how-to-run-your-own-e-mail-server-with-your-own-domain-part-1/) will recommend notqmail.

[notqmail](http://notqmail.org) is a community-driven fork of [qmail](https://cr.yp.to/qmail.html), beginning where [netqmail](http://netqmail.org) left off: providing stable, compatible, small releases to which existing qmail users can safely update. notqmail also aims higher: developing an extensible, easily packaged, and increasingly useful modern mail server.

The current release is [[notqmail 1.08]], issued 20 May 2020.


# Why not Postfix?

_We know you're wondering._

[Postfix](http://www.postfix.org) is very good. We also really like qmail.

For now, we're targeting sysadmins who already run a qmail-based mail system. If it's not clear to you why you'd run notqmail instead of Postfix, you're probably right. Someday, when notqmail is more featureful, we'll want to compare and contrast with other MTAs. In the meantime, many of [qmail 1.03's advantages](https://cr.yp.to/qmail.html) are still relevant.


# Why should I trust notqmail?

_Watch what we do and how we do it; then decide._

This is a big question and it deserves a [[thorough answer|Trust]].


# Are DJB or any of the netqmail authors involved?

_We'd love to have them, of course._

Neither netqmail nor DJB were asked to approve of this distribution.


# Does the [qmail security guarantee](https://cr.yp.to/qmail/guarantee.html) apply?

_We do warrant that we've made a good-faith attempt to ensure that the software behaves correctly._

Sorry, no. We're not DJB, and notqmail is not qmail.


# What are the project's goals?

See [[Goals and Non-Goals]].


# Which features will eventually be implemented?

_All the important ones._

Some known big ones:

- SMTP recipient validation
- TLS
- AUTH
- IPv6
- SPF
- SRS
- DKIM
- DMARC
- EAI
- SNI

Need something else? Tell us about it. 

Our [[roadmap]] describes our plans in somewhat more detail.


# Which implementations won't last forever?

_Some designs are more _qmail_ than others._

There are many, many patches out there. Needless to say, not all of them meet notqmail's design goals. Two examples of popular, well-loved patches we've personally used and appreciated that could make useful "extensions" starting with 1.9, but would likely be superseded in the course of time:

- The [Qmail-TLS patch](http://inoa.net/qmail-tls/), because a more qmail-ish design is available: [Erwin Hoffmann's ucspi-ssl](https://www.fehcom.de/ipnet/ucspi-ssl.html) implements UCSPI-TLS, handling TLS in a separate and privilege-separated address space
- Any of the usual SMTP AUTH patches, because a more qmail-ish design is available: [Amitai Schleier's acceptutils](https://schmonz.com/qmail/acceptutils/) extends qmail's POP3 authentication architecture to SMTP and OFMIP, enabling new user-controlled features

For some elaborated examples we might choose to follow, see [[Designs]].


# What happens to my custom patchset?

_Patience._

Expect your patchset to:

- Mostly continue to apply
- Gradually shrink as new notqmail releases include more of the features and bugfixes you need
- Eventually shrink to zero, if your needs are widely shared by others

For more, see [[Patches]].


# How do I install notqmail?

_It's not incapable of installing to `/var/qmail`._

Your build scripts will continue to work.
We've tested many [[platforms]].
See [[Install]].


# How can I get more involved?

_Be part of the revival!_

Our [git repository](https://github.com/notqmail/notqmail) and [issue tracker](https://github.com/notqmail/notqmail/issues) are hosted by GitHub.  Various contributors to notqmail are active on the [qmail mailing list](https://cr.yp.to/lists.html#qmail) and on [Freenode's](https://freenode.net/) `#qmail` IRC channel.

We invite users or enthusiasts of qmail to join us. We especially hope for:

- Ideas and feedback from those of you running (or not quite running) qmail
- Code from those of you with custom patchsets or forks

Say hi on the list or IRC and one of us will help you get started on your first contribution.