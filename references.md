[[!meta title="References"]]

Code and documents relevant to the design, implementation, and use of notqmail.


## Other forks of qmail

- [netqmail](http://netqmail.org)
- [mbhangui](https://github.com/mbhangui)'s [IndiMail](https://github.com/mbhangui/indimail-mta)
- [Erwin Hoffmann](https://github.com/ErwinHo)'s [s/qmail](https://www.fehcom.de/sqmail/sqmail.html)
- [Kai Peter](https://github.com/kp-org)'s [eQmail](https://github.com/kp-org/eQmail)
- [DerDakon](https://github.com/DerDakon)'s [qmail](https://github.com/DerDakon/qmail)
- [schmonz](https://github.com/schmonz)'s [qmail](https://github.com/schmonz/qmail)


## Other sources of patches

- [qmail.org](https://qmail.notqmail.org/top.html)
- Debian's [netqmail](https://sources.debian.org/src/netqmail/)
- pkgsrc's [qmail](https://github.com/NetBSD/pkgsrc/tree/trunk/mail/qmail) and [qmail-run](https://github.com/NetBSD/pkgsrc/tree/trunk/mail/qmail-run)
- [schmonz](https://github.com/schmonz)'s [patch page](https://schmonz.com/qmail/)
- [Roberto Puzzanghera](https://github.com/sagredo-dev)'s [qmail notes](https://notes.sagredo.eu)
- John M. Simpson's [combined patch](https://qmail.jms1.net/patches/combined-details.shtml)
- [Bruce Guenter](https://github.com/bruceg)'s [software page](http://untroubled.org/software.php)
- [Kyle Wheeler](https://github.com/m3m0ryh0l3)'s [Qmail Patch Explanations and Recommendations](http://www.memoryhole.net/qmail/)
- [Scott Gifford](https://github.com/scottgifford)'s original [UCSPI-TLS implementation](https://github.com/SuperScript/ucspi-ssl/pull/1) (including `sslclient -y`, not yet merged in [Erwin Hoffmann](https://github.com/ErwinHo)'s [ucspi-ssl](https://www.fehcom.de/ipnet/ucspi-ssl.html)) and [specification](https://web.archive.org/web/20150311223927/http://www.suspectclass.com/sgifford/ucspi-tls/)
- Frederik Vermeulen's [Qmail-TLS patch](http://inoa.net/qmail-tls/)
- Eben Pratt's [list of recipient checkers](http://www.netdevice.com/qmail/rcptck)


## Add-ons

- [schmonz](https://github.com/schmonz)'s [acceptutils](https://schmonz.com/qmail/acceptutils)
- [schmonz](https://github.com/schmonz)'s [rejectutils](https://schmonz.com/qmail/rejectutils)
- [DerDakon](https://github.com/DerDakon)'s [Qsmtp](https://github.com/DerDakon/Qsmtp)
- [Jan Mojžíš](https://github.com/janmojzis)'s [qremote](https://mojzis.com/software/qremote/)


## Community Wisdom

- [josuah's notqmail site](https://notqmail.z0.is/)
- Dave Sill, 2007: [Life with qmail](http://www.lifewithqmail.org/lwq.html)
- Wayne Marshall, 2007: [the djb way](http://thedjbway.b0llix.net/index.html)
- Henning Brauer, 2004: [Life With qmail-ldap](http://www.lifewithqmail.org/ldap/)
- [NO STARTTLS](https://nostarttls.secvuln.info)
- [SMTP Smuggling](https://sec-consult.com/blog/detail/smtp-smuggling-spoofing-e-mails-worldwide/)

## Papers

- Daniel J. Bernstein, 2007: [Some thoughts on security after ten years of qmail 1.0](https://cr.yp.to/qmail/qmailsec-20071101.pdf)


## Talks and Podcasts

- [schmonz](https://github.com/schmonz), Wed Jan 8 2020: [What is notqmail?](https://schmonz.com/talk/2020-nyc-january/)
- [schmonz](https://github.com/schmonz), Fri Jan 10 2020: [Programming Leadership: Collaboration and Notqmail with Amitai Schleier](https://schmonz.com/talk/20200110-programming-leadership/)


## News & Social Media

### 1.08

- Linux Weekly News, Wed 20 May 2020: [A remote code execution vulnerability in qmail](https://lwn.net/Articles/820969/)
- golem.de, Wed 20 May 2020: [Sicherheitslücke in Qmail](https://www.golem.de/news/remote-code-execution-sicherheitsluecke-in-qmail-2005-148613.html) (German, "Vulnerability in Qmail")
- Lobste.rs, Wed 20 May 2020: [notqmail 1.08 released](https://lobste.rs/s/bdq0di/notqmail_1_08_released)
- Hacker News, Wed 20 May 2020: [Notqmail 1.08 released](https://news.ycombinator.com/item?id=23252421)
- Help Net Security, Wed 20 May 2020: [Vulnerability in Qmail mail transport agent allows RCE](https://www.helpnetsecurity.com/2020/05/20/qmail-rce/)
- Hacker News, Tue 19 May 2020: [15 years later: Remote Code Execution in qmail (CVE-2005-1513)](https://news.ycombinator.com/item?id=23237716)
- Lobste.rs, Tue 19 May 2020: [Remote Code Execution in qmail (CVE-2005-1513)](https://lobste.rs/s/ercmor/remote_code_execution_qmail_cve_2005_1513)
- qualys.com, Tue 19 May 2020: [15 years later: Remote Code Execution in qmail](https://www.qualys.com/2020/05/19/cve-2005-1513/remote-code-execution-qmail.txt)

### 1.07

- mag.osdn.jp, Fri 23 Aug 2019: [コミュニティ主導のqmailフォークプロジェクト「notqmail」が立ち上げられる](https://mag.osdn.jp/19/08/23/160000.amp) (Japanese, "Community-led qmail fork project 'notqmail' launched")
- linux-magazin.de, Thu 22 Aug 2019: [Notqmail forkt Qmail](https://www.linux-magazin.de/news/notqmail-forkt-qmail/) (German, "notqmail forks qmail")
- linux-os.net, Thu 22 Aug 2019: [Notqmail una bifurcación de qmail](https://linux-os.net/notqmail-una-bifurcacion-de-qmail/) (Spanish, "notqmail, a fork of qmail")
- opennet.ru, Wed 21 Aug 2019: [Представлен notqmail, форк почтового сервера qmail](https://www.opennet.ru/opennews/art.shtml?num=51326) (Russian, "notqmail introduced, fork of qmail mail server")
- pro-linux.de, Wed 21 Aug 2019: [notqmail will Qmail-Forks konsolidieren](https://www.pro-linux.de/news/1/27365/notqmail-will-qmail-forks-konsolidieren.html) (German, "notqmail wants to consolidate qmail forks")
- Reddit /r/GCU_Squad, Tue 20 Aug 2019: [Announcing the initial 1.07 release of notqmail, a community-driven fork of qmail](https://www.reddit.com/r/GCU_Squad/comments/ct0o89/announcing_the_initial_107_release_of_notqmail_a/)
- Hacker News, Tue 20 Aug 2019: [Announcing notqmail](https://news.ycombinator.com/item?id=20752671)
- Linux Weekly News, Tue 20 Aug 2019: [Announcing notqmail](https://lwn.net/Articles/796794/)
- Lobste.rs, Tue 20 Aug 2019: [notqmail-1.07: portability and correctness, binary packaging release](https://lobste.rs/s/kvsqqr/notqmail_1_07_portability_correctness)
- A Fresh Cup, Wed 07 Aug 2019: [Double Shot #2402](https://afreshcup.com/home/2019/08/07/double-shot-2402.html)
- GeekLAN, Mon 29 Jul 2019: [Something blogged (on pkgsrcCon 2019)](https://www.geeklan.co.uk/?p=2392)
- O'Reilly, Mon 29 Jul 2019: [Four short links, Nat Torkington](https://www.oreilly.com/ideas/four-short-links-29-july-2019)
- Lobste.rs, Sun 28 Jul 2019: [Notqmail: Collaborative open-source successor to qmail](https://lobste.rs/s/2r3stk/notqmail_collaborative_open_source)
- Hacker News, Sun 28 Jul 2019: [Notqmail: Collaborative open-source successor to qmail](https://news.ycombinator.com/item?id=20549983)

### Pre-notqmail

- Russ Nelson, 2007: [netqmail 1.06](https://marc.info/?l=qmail&m=119689105301544&w=2)
