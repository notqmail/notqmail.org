# What is notqmail?

> It's not [qmail](https://cr.yp.to/qmail.html) and it's not [netqmail](http://netqmail.org).

[notqmail](http://notqmail.org) is a community-driven fork of qmail, the well-known Unix [mail transfer agent](https://en.wikipedia.org/wiki/Message_transfer_agent) (MTA). notqmail begins where netqmail left off: we will provide stable, compatible, small releases that do not conflict with or break your local site customization or the other software you run in your mail system. notqmail also aims higher: we are developing a qmail-derived system that is extensible, easily packaged, and increasingly applicable to a wide variety of modern needs.

notqmail is an email _server_. We all have email, so we all have email servers. Someday, if we do a good job, [articles explaining why and how to run your own](https://arstechnica.com/information-technology/2014/02/how-to-run-your-own-e-mail-server-with-your-own-domain-part-1/) will recommend notqmail. But first, we have to prove we're a worthy upgrade path for people who are already running qmail or netqmail.

# How to install notqmail

> It's not incapable of installing to `/var/qmail`.

The release notes for [[notqmail-1.07]] describe how to install notqmail.  Your existing qmail build scripts still work.

# Release roadmap

> We have big plans.

Our [[release roadmap|Release-Roadmap]] describes when we plan on releasing particular features, and our [[tested distributions|Tested-Distributions]] show which platforms we've built, tested, or run notqmail on.
The notqmail git repository contains an import of qmail and netqmail, with tags or branches at each historical release. notqmail is a fork of netqmail 1.06.

# Why should I trust notqmail?

> Watch what we do and how we do it; then decide.

We trust qmail, as you do, for at least these reasons:

1. Simple, elegant design
2. Very few bugs
3. Stable in production

It's for these reasons that we're motivated to continue developing qmail to meet modern needs.

DJB's code was trustworthy. netqmail's small, conservative patchset was trustworthy. We intend for our development process to be trustworthy. If you find otherwise, we'd be extremely grateful to hear your doubts and concerns. But if you decide we're being consistently careful, thoughtful, reasonable, and practical, we hope you'll update to notqmail.

# What happens to my custom patchset?

> Patience.

Expect your patchset to:

- Mostly continue to apply
- Gradually shrink as new notqmail releases include more of the features and bugfixes you need
- Eventually shrink to zero, if your needs are widely shared by others

In other words, you can stop maintaining your qmail fork as soon as notqmail has everything you need (which may take longer than you expect). Until then, keep it. And if you're interested to participate in notqmail development, sharing your needs and/or patches is a great place to start.

# Which features will be implemented?

> All the important ones. Eventually.

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
- DANE

Need something else? Tell us about it.

# Which implementations probably won't win?

> Some designs are more _qmail_ than others.

There are many, many patches out there. Needless to say, not all of them meet notqmail's design goals. Two examples of popular, well-loved patches we've personally used and appreciated that could make useful "extensions" (planned for notqmail-1.1), but would almost certainly be superseded in the course of time by other implementations:

- The [Qmail-TLS patch](http://inoa.net/qmail-tls/), because a more qmail-ish design is available: [Erwin Hoffmann's ucspi-ssl](https://www.fehcom.de/ipnet/ucspi-ssl.html) implements UCSPI-TLS, handling TLS in a separate and privilege-separated address space
- Any of the usual SMTP AUTH patches, because a more qmail-ish design is available: [Amitai Schleier's acceptutils](https://schmonz.com/qmail/acceptutils/) extends qmail's POP3 authentication architecture to SMTP and OFMIP, enabling new user-controlled features

# Goals

> We'll trade away other things to get these.

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

> We'll trade very little of these to get other things.

We wish to avoid:

- Breaking compatibility
- Breaking existing features of the architecture
- Modifying or replacing core components

Given the reasons qmail is valuable to us, the cost of a change that exhibits any of the preceding non-goals is high. Proposing one such change will require unusually strong justification, documentation, testing, and design. For the community to accept such a change, the risk must be demonstrably _very_ low and the benefit _very_ high.

# Getting involved

> Be part of the revival!

Our [git repository](https://github.com/notqmail/notqmail) and [issue tracker](https://github.com/notqmail/notqmail/issues) are hosted by GitHub.  Various contributors to notqmail are active on the [qmail mailing list](https://cr.yp.to/lists.html#qmail) and on [Freenode's](https://freenode.net/) `#qmail` IRC channel.

We invite users or enthusiasts of qmail to join us. We especially hope for:

- Ideas and feedback from those of you running (or not quite running) qmail
- Code from those of you with custom patchsets or forks

Say hi on the list or IRC and one of us will help you get started on your first contribution.

# Are djb or any of the netqmail authors involved?

> We'd love to have them, of course.

Neither netqmail nor djb were asked to approve of this distribution.

# Why not Postfix?

> We know you're wondering.

[Postfix](http://www.postfix.org) is very good. We also really like qmail.