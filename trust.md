[[!meta title="Trust"]]

## Why should I trust notqmail?

We have come to trust qmail, as you have, for at least these reasons:

1. Simple, elegant design
2. Very few bugs
3. Stable in production

It's for these reasons that we're motivated to continue developing qmail to meet modern needs.

None of us can do what [DJB](https://cr.yp.to/djb.html) did. One mitigating factor here is, we're not trying to do what DJB did. He had to write qmail from scratch; we have the advantage of existing designs, interfaces, implementations, and decades of running in production. We also enjoy the privilege of using the latest techniques and tooling. But the two biggest mitigations we have are:

1. Working in public
2. Shipping frequent small releases

"Working in public" means we're thinking out loud, showing our work, reacting to reviewer feedback, and making our decision-making process as explicit as possible.

"Shipping frequent small releases" means

- Our previous release will always have been fairly recent, so we'll remember how to do it carefully
- Our next release is always fairly soon, so we'll design and review a little extra carefully
- Any given release contains relatively few changes, so our users can probably vet them a little extra carefully

None of us can hold in mind all simultaneous details the way it seems DJB must have. As a community, though, we might manage to make very few terrible mistakes that survive for long.

DJB's code was trustworthy. netqmail's small, conservative patchset was trustworthy. We intend for our development process to be trustworthy. If you find otherwise, we'd be extremely grateful to hear your doubts and concerns. But if you decide we're being consistently careful, thoughtful, reasonable, and practical, we hope you'll update to notqmail.

Our starting point for this project is [netqmail 1.06](https://github.com/notqmail/notqmail/tree/netqmail-1.06), with previous netqmail and qmail releases also tagged in the repo.
