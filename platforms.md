[[!meta title="Platforms"]]

Every proposed change is
[automatically tested](https://github.com/notqmail/notqmail/actions?query=workflow%3ABuild)
on the widest possible variety of operating systems and hardware architectures available on GitHub.
If a PR doesn't pass tests everywhere, it doesn't get merged.

Test coverage isn't as good as we'd like.
For instance, `TEST.deliver` and `TEST.receive` aren't yet part of automated test runs.

We supplement GitHub's assurances with occasional manual testing on platforms we can access directly.
Some past results are listed below.

(It'd be cool to have our platform statuses updated automatically at some point.)

## [[notqmail 1.07|releases/1.07]]

Help us fill this in!

### amd64 ELF

[[!table data="""
Platform     | Version      | [[Build+Package|install]] | [TEST.deliver](https://github.com/notqmail/notqmail/blob/master/TEST.deliver) | [TEST.receive](https://github.com/notqmail/notqmail/blob/master/TEST.receive) | In Prod
Alpine Linux |       3.10.0 |               |              |              |
Arch Linux   |   2019.07.01 |               |              |              |
CentOS       |            6 | y+pkgsrc      | y+pkgsrc     |              |
CentOS       |            7 | y+pkgsrc      | y+pkgsrc     |              | @alanpost
Debian       |      Jesse 8 |               |              |              |
Debian       |    Stretch 9 | y+pkgsrc      | y+pkgsrc     |              |
Devuan       |            2 | y+pkgsrc      | y+pkgsrc     |              |
Fedora       |           29 |               |              |              |
Fedora       |           30 | y             |              |              |
FreeBSD      |         11.2 |               |              |              |
FreeBSD      |         12.0 | y+pkgsrc      | y+pkgsrc     |              |
Gentoo       |              | y+Gentoo patches | y+Gentoo  | y+Gentoo     | @DerDakon
NetBSD       |          9.2 | y+pkgsrc      | y+pkgsrc     | y+pkgsrc     | @schmonz
NixOS        |        19.03 |               |              |              |
OpenBSD      |          6.5 | y+pkgsrc      | y+pkgsrc     |              | @xenotrope
Tribblix     |       0m20.5 | y+pkgsrc      | y+pkgsrc     |              |
Ubuntu       | Trusty 14.04 |               |              |              |
Ubuntu       | Xenial 16.04 | y+pkgsrc      | y+pkgsrc     |              |
Ubuntu       | Bionic 18.04 |               |              |              |
Ubuntu       |  Disco 19.04 |               |              |              |
Void Linux   |    4.19.66_1 | y+pkgsrc      | y+pkgsrc     |              |
"""]]

### amd64 Mach-O

[[!table data="""
Platform     | Version      | [[Build+Package|install]] | [TEST.deliver](https://github.com/notqmail/notqmail/blob/master/TEST.deliver) | [TEST.receive](https://github.com/notqmail/notqmail/blob/master/TEST.receive) | In Prod
macOS        | Sierra 10.12 |               |              |              |
macOS        | Mojave 10.14 | y+pkgsrc      | y+pkgsrc     |              |
macOS        | Big Sur 11.5 | y+pkgsrc      | y+pkgsrc     |              |
"""]]

### aarch64 Mach-O

[[!table data="""
Platform     | Version      | [[Build+Package|install]] | [TEST.deliver](https://github.com/notqmail/notqmail/blob/master/TEST.deliver) | [TEST.receive](https://github.com/notqmail/notqmail/blob/master/TEST.receive) | In Prod
macOS        | Big Sur 11.5 | y+pkgsrc      | y+pkgsrc     |              |
"""]]

### aarch64 ELF

[[!table data="""
Platform     | Version      | [[Build+Package|install]] | [TEST.deliver](https://github.com/notqmail/notqmail/blob/master/TEST.deliver) | [TEST.receive](https://github.com/notqmail/notqmail/blob/master/TEST.receive) | In Prod
NetBSD       | 9.2          | y+pkgsrc      | y+pkgsrc     |              |
Ubuntu       | Bionic 18.04 | y+pkgsrc      | y+pkgsrc     |              |
"""]]

### hppa ELF

[[!table data="""
Platform     | Version      | [[Build+Package|install]] | [TEST.deliver](https://github.com/notqmail/notqmail/blob/master/TEST.deliver) | [TEST.receive](https://github.com/notqmail/notqmail/blob/master/TEST.receive) | In Prod
Gentoo       |              | y+Gentoo patches | y+Gentoo  | y+Gentoo     | @DerDakon
"""]]

### pmax ELF

[[!table data="""
Platform     | Version      | [[Build+Package|install]] | [TEST.deliver](https://github.com/notqmail/notqmail/blob/master/TEST.deliver) | [TEST.receive](https://github.com/notqmail/notqmail/blob/master/TEST.receive) | In Prod
NetBSD       |          8.1 | y             |              |              |
"""]]

### sparc ELF

[[!table data="""
Platform     | Version      | [[Build+Package|install]] | [TEST.deliver](https://github.com/notqmail/notqmail/blob/master/TEST.deliver) | [TEST.receive](https://github.com/notqmail/notqmail/blob/master/TEST.receive) | In Prod
Gentoo       |              | y+Gentoo patches | y+Gentoo  | y+Gentoo     | @DerDakon
"""]]
