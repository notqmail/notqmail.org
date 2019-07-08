# What is notqmail?

It's not [qmail](https://cr.yp.to/qmail.html). It's also not [netqmail](http://netqmail.org).

notqmail is a collaborative effort by qmail devotees to defend what's valuable, add what's needed, and ship trustworthy updates everyone can run.

# Are DJB and/or any of the netqmail authors involved?

No. We'd be extremely happy to have them, of course.

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

# Why not Postfix?

[Postfix](http://www.postfix.org) is very good. We also really like qmail.

# What happens to my custom patchset?

Expect your patchset to

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

# Which implementations will not be merged?

There are many, many patches out there. Needless to say, not all of them are suitable for inclusion in notqmail. Two examples of popular, well-loved patches we've personally used and appreciated that don't match notqmail's goals:

- The [Qmail-TLS patch](http://inoa.net/qmail-tls/), because a more qmail-ish design is available: [Erwin Hoffmann's ucspi-ssl](https://www.fehcom.de/ipnet/ucspi-ssl.html) implements UCSPI-TLS, handling TLS in a separate and privilege-separated address space
- Any of the usual SMTP AUTH patches, because a more qmail-ish design is available: [Amitai Schleier's acceptutils](https://schmonz.com/qmail/acceptutils/) extends qmail's POP3 authentication architecture to SMTP and OFMIP, enabling new user-controlled features

# Goals

We prioritize:

- Implementing new features (or alternatives to core components) as "plugins"
- Adding interfaces and seams, where needed, to make plugins possible
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

- Breaking compatibility (such as by moving away from `/var/qmail`)
- Breaking existing features of the architecture
- Modifying or replacing core components

Given the reasons qmail is valuable to us, the cost of such a change is high. Proposing one such change will require unusually strong justification, documentation, testing, and design. For the community to accept such a change, the risk must be demonstrably _very_ low and the benefit _very_ high.

# First steps

We intend to:

- Import qmail and netqmail into git, with tags at each historical version.
- Release notqmail 1.07: bit-identical to netqmail 1.06.
- Add new interfaces and seams for use by future "plugins".
- Release notqmail 1.08: no functional change.
- Help several developers of active qmail forks each get one notqmail plugin (adapted from their existing code) committed.
- Release notqmail 1.09: our first few plugins for new functionality.
- Help developers convert more of their existing code to plugins.
- Release notqmail 1.10: several more new plugins.
- Keep it up.

# How to join

We're active on the [qmail mailing list](https://cr.yp.to/lists.html#qmail) and on Freenode `#qmail`. If you're reading this, you've found our GitHub repo. (We'll have a separate list where our commits get sent.)

Say hi on the list and/or IRC and one of us will help you get started on your first contribution.

# How to install

Wait for our first notqmail release. Then build and install it just like qmail.