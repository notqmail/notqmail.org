[[!meta title="Feature Wishlist"]]

## Which features will eventually be implemented?

Some known big ones:

- SMTP recipient validation
- TLS
- AUTH
- IPv6
- SPF
- SRS
- DKIM
- DMARC
- ARC
- EAI
- SNI
- DANE
- MTA-STS

Need something else? Tell us about it.

Our [[roadmap]] describes our plans in somewhat more detail.


## Which implementations won't last forever?

There are many, many [[patches]] out there. Needless to say, not all of them meet notqmail's design goals. Two examples of popular, well-loved patches we've personally used and appreciated whose features we hope to provide in other ways:

- The [Qmail-TLS patch](http://inoa.net/qmail-tls/), because a more qmail-ish design is available: [UCSPI-TLS](https://www.fehcom.de/ipnet/ucspi-ssl/man/ucspi-tls.2.html) (implemented in [s6-networking](https://skarnet.org/software/s6-networking/) and [ucspi-ssl](https://www.fehcom.de/ipnet/ucspi-ssl.html)) extends [UCSPI](https://cr.yp.to/proto/ucspi.txt) to provide opportunistic TLS for client and server applications in a separate and privilege-separated address space
- Any of the usual SMTP AUTH patches, because a more qmail-ish design is available: [Amitai Schleier's acceptutils](https://schmonz.com/qmail/acceptutils/) extends qmail's POP3 authentication architecture to SMTP and OFMIP, enabling new user-controlled features

See also [[Designs]].
