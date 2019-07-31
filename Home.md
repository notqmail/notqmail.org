# What is notqmail?

_It's not qmail. It's also not netqmail._

We all use email, so we all use email servers. notqmail is software for running an [email server](https://en.wikipedia.org/wiki/Message_transfer_agent). Someday, if we do a good job, some of the many [articles about how and why to run your own](https://arstechnica.com/information-technology/2014/02/how-to-run-your-own-e-mail-server-with-your-own-domain-part-1/) will recommend notqmail.

[notqmail](http://notqmail.org) is a community-driven fork of [qmail](https://cr.yp.to/qmail.html). notqmail begins where [netqmail](http://netqmail.org) left off: providing stable, compatible, small releases to which existing qmail users can safely update. notqmail also aims higher: developing an extensible, easily packaged, and increasingly useful modern mail server.


# Why should I trust notqmail?

_Watch what we do and how we do it; then decide._

We have come to trust qmail, as you have, for at least these reasons:

1. Simple, elegant design
2. Very few bugs
3. Stable in production

It's for these reasons that we're motivated to continue developing qmail to meet modern needs.

DJB's code was trustworthy. netqmail's small, conservative patchset was trustworthy. We intend for our development process to be trustworthy. If you find otherwise, we'd be extremely grateful to hear your doubts and concerns. But if you decide we're being consistently careful, thoughtful, reasonable, and practical, we hope you'll update to notqmail.

Our starting point for this project is [netqmail 1.06](https://github.com/notqmail/notqmail/tree/netqmail-1.06), with previous netqmail and qmail releases also tagged in the repo.


# What are the project's goals?

_We'll trade away other things to get these._

We prioritize:

- Implementing new features (or alternatives to core components) as "extensions"
- Adding interfaces and seams, where needed, to make extensions possible
- Encouraging multiple initial implementations of X, for any X
- Following consensus, merging the best aspects into one implementation
- Providing sensible defaults and easily configured runtime options
- Providing a safe update path for qmail and netqmail users
- Providing safe, easy, regular updates for notqmail users
- Gradually reducing the marginal cost of developing notqmail
- Being easily packaged by OS integrators
- Meeting all common needs with OS-provided packages
- Earning community trust as the authoritative open-source successor to qmail and netqmail


# What are the project's non-goals?

_We'll trade very little of these to get other things._

We wish to avoid:

- Breaking compatibility
- Breaking your patches
- Breaking existing features of the architecture
- Modifying or replacing core components

Given the reasons qmail is valuable to us, the cost of a change that exhibits any of the preceding non-goals is high. Proposing one such change will require unusually strong justification, documentation, testing, and design. For the community to accept such a change, the risk must be demonstrably _very_ low and the benefit _very_ high.


# Which features will eventually be implemented?

_All the important ones._

Some known big ones:

- SMTP recipient validation
- AUTH
- TLS
- SPF
- SRS
- DKIM
- DMARC
- EAI
- SNI

Need something else? Tell us about it. 

Our [[release roadmap|Release-Roadmap]] describes our plans in somewhat more detail.


# Which implementations won't last forever?

_Some designs are more _qmail_ than others._

There are many, many patches out there. Needless to say, not all of them meet notqmail's design goals. Two examples of popular, well-loved patches we've personally used and appreciated that could make useful "extensions" starting with 1.9, but would likely be superseded in the course of time:

- The [Qmail-TLS patch](http://inoa.net/qmail-tls/), because a more qmail-ish design is available: [Erwin Hoffmann's ucspi-ssl](https://www.fehcom.de/ipnet/ucspi-ssl.html) implements UCSPI-TLS, handling TLS in a separate and privilege-separated address space
- Any of the usual SMTP AUTH patches, because a more qmail-ish design is available: [Amitai Schleier's acceptutils](https://schmonz.com/qmail/acceptutils/) extends qmail's POP3 authentication architecture to SMTP and OFMIP, enabling new user-controlled features


# What happens to my custom patchset?

_Patience._

Expect your patchset to:

- Mostly continue to apply
- Gradually shrink as new notqmail releases include more of the features and bugfixes you need
- Eventually shrink to zero, if your needs are widely shared by others

In other words, you can stop maintaining your qmail fork as soon as notqmail has everything you need (which may take longer than you expect). Until then, keep it. And if you're interested to participate in notqmail development, sharing your needs and/or patches is a great place to start.


# How do I install notqmail?

_It's not incapable of installing to `/var/qmail`._

Your existing build scripts will still work. 
We've [[tested many platforms|Tested-Distributions]].
See [[notqmail-1.07]].


# How can I get more involved?

_Be part of the revival!_

Our [git repository](https://github.com/notqmail/notqmail) and [issue tracker](https://github.com/notqmail/notqmail/issues) are hosted by GitHub.  Various contributors to notqmail are active on the [qmail mailing list](https://cr.yp.to/lists.html#qmail) and on [Freenode's](https://freenode.net/) `#qmail` IRC channel.

We invite users or enthusiasts of qmail to join us. We especially hope for:

- Ideas and feedback from those of you running (or not quite running) qmail
- Code from those of you with custom patchsets or forks

Say hi on the list or IRC and one of us will help you get started on your first contribution.


# Are djb or any of the netqmail authors involved?

_We'd love to have them, of course._

Neither netqmail nor djb were asked to approve of this distribution.


# Why not Postfix?

_We know you're wondering._

[Postfix](http://www.postfix.org) is very good. We also really like qmail.