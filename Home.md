# What is notqmail?

_---It's not [qmail](https://cr.yp.to/qmail.html). It's also not [netqmail](http://netqmail.org).---_

notqmail, a Unix mail transfer agent (MTA), is a fork of qmail in the netqmail family.  notqmail is a community-assembled distribution to provide an extensible, packaged qmail.  Our goal is to provide stable, compatible, regular releases that will not break or conflict with your site customization.

# Release plans

We've imported qmail and netqmail into git, with tags at each historical version. Our starting point for notqmail is netqmail 1.06. Read more about [our release roadmap](https://github.com/notqmail/notqmail/wiki/Release-Plans).

# Who is involved?

We invite everyone to join us. We especially hope for:

- Ideas and feedback from those of you running (or not quite running) qmail
- Code from those of you with custom patchsets or forks

# Why should I trust notqmail?

We trust qmail, as you do, for at least these reasons:

1. Simple, elegant design
2. Very few bugs
3. Stable in production

It's for these reasons that we're motivated to continue developing qmail to meet modern needs.

DJB's code was trustworthy. netqmail's small, conservative patchset was trustworthy. We intend for our development process to be trustworthy. If you find otherwise, we'd be extremely grateful to hear your doubts and concerns. But if you decide we're being consistently careful, thoughtful, reasonable, and practical, we hope you'll update to notqmail.

# What happens to my custom patchset?

Expect your patchset to:

- Mostly continue to apply
- Gradually shrink as new notqmail releases include more of the features and bugfixes you need
- Eventually shrink to zero, if your needs are widely shared by others

In other words, you can stop maintaining your qmail fork as soon as notqmail has everything you need (which may take longer than you expect). Until then, keep it. And if you're interested to participate in notqmail development, sharing your needs and/or patches is a great place to start.

# Which features will be implemented?

Some known big ones:

- AUTH
- TLS
- SPF
- SRS
- DKIM
- DMARC
- EAI
- SNI
- DANE

Need something else? Tell us about it.

# Which implementations probably won't win?

There are many, many patches out there. Needless to say, not all of them meet notqmail's design goals. Two examples of popular, well-loved patches we've personally used and appreciated that could make useful "extensions" (planned for notqmail-1.1), but would almost certainly be superseded in the course of time by other implementations:

- The [Qmail-TLS patch](http://inoa.net/qmail-tls/), because a more qmail-ish design is available: [Erwin Hoffmann's ucspi-ssl](https://www.fehcom.de/ipnet/ucspi-ssl.html) implements UCSPI-TLS, handling TLS in a separate and privilege-separated address space
- Any of the usual SMTP AUTH patches, because a more qmail-ish design is available: [Amitai Schleier's acceptutils](https://schmonz.com/qmail/acceptutils/) extends qmail's POP3 authentication architecture to SMTP and OFMIP, enabling new user-controlled features

# Goals

_---We're capable of installing in to /var/qmail---_

We prioritize:

- Implementing new features (or alternatives to core components) as "extensions"
- Adding interfaces and seams, where needed, to make extensions possible
- Encouraging multiple initial implementations of X, for any X
- Following consensus, merging the best aspects into one implementation
- Providing sensible defaults and easily configured runtime options
- Providing a safe update path for qmail and netqmail users
- Providing safe, easy, regular updates for notqmail users
- Being easily packaged by OS integrators
- Meeting all common needs with OS-provided packages
- Earning community trust as the authoritative open-source successor to qmail and netqmail

# Non-goals

We wish to avoid:

- Breaking compatibility
- Breaking existing features of the architecture
- Modifying or replacing core components

Given the reasons qmail is valuable to us, the cost of a change that exhibits any of the preceding non-goals is high. Proposing one such change will require unusually strong justification, documentation, testing, and design. For the community to accept such a change, the risk must be demonstrably _very_ low and the benefit _very_ high.

# How to join

We're active on the [qmail mailing list](https://cr.yp.to/lists.html#qmail) and on [Freenode's](https://freenode.net/) `#qmail`. If you're reading this, you've found our GitHub repo. (We'll have a separate list where our commits get sent.)

Say hi on the list and/or IRC and one of us will help you get started on your first contribution.

# How to install

Wait for our first notqmail release. Then build and install it just like qmail.

# Are djb or any of the netqmail authors involved?

Neither netqmail nor djb were asked to approve of this distribution.

# Why not Postfix?

[Postfix](http://www.postfix.org) is very good. We also really like qmail.