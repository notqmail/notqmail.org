The following distributions have been tested with notqmail:

_NOTE: Entries without a Build+Package entry are a call for testing._

| Distribution | Version      | Arch  | BinFmt | Build+Package | TEST.deliver | TEST.receive | Running |
| ------------ | -----------: | ----- | ------ | ------------: | -----------: | -----------: | ------: |
| Alpine Linux |       3.10.0 | amd64 | elf    |               |              |              |         |
| Arch Linux   |   2019.07.01 | amd64 | elf    |               |              |              |         |
| CentOS       |            6 | amd64 | elf    |               |              |              |         |
| CentOS       |            7 | amd64 | elf    | notqmail-1.07 |              |              |       y |
| Debian       |      Jesse 8 | amd64 | elf    |               |              |              |         |
| Debian       |    Stretch 9 | amd64 | elf    |               |              |              |         |
| Devuan       |            2 | amd64 | elf    |               |              |              |         |
| Fedora       |           29 | amd64 | elf    |               |              |              |         |
| Fedora       |           30 | amd64 | elf    | notqmail-1.07 |              |              |         |
| FreeBSD      |         11.2 | amd64 | elf    |               |              |              |         |
| FreeBSD      |         12.0 | amd64 | elf    |               |              |              |         |
| Gentoo       |              | amd64 | elf    | notqmail-1.07 + Gentoo patches | 1.07+Gentoo | 1.07+Gentoo | y |
| Gentoo       |              | hppa  | elf    | notqmail-1.07 + Gentoo patches | 1.07+Gentoo | 1.07+Gentoo | y |
| Gentoo       |              | sparc | elf    | notqmail-1.07 + Gentoo patches | 1.07+Gentoo | 1.07+Gentoo | y |
| Mac OS X     | Sierra 10.12 | amd64 | mach-o |               |              |              |         |
| Mac OS X     | Mojave 10.14 | amd64 | mach-o |               |              |              |         |
| NetBSD       |          8.1 | amd64 | elf    |               |              |              |         |
| NixOS        |        19.03 | amd64 | elf    |               |              |              |         |
| OpenBSD      |          6.5 | amd64 | elf    |               |              |              |         |
| Tribblix     |       0m20.5 | amd64 | elf    |               |              |              |         |
| Ubuntu       | Trusty 14.04 | amd64 | elf    |               |              |              |         |
| Ubuntu       | Xenial 16.04 | amd64 | elf    |               |              |              |         |
| Ubuntu       | Bionic 18.04 | amd64 | elf    |               |              |              |         |
| Ubuntu       |  Disco 19.04 | amd64 | elf    |               |              |              |         |