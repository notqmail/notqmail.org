[[!meta title="Goals and Non-Goals"]]

## What are notqmail's goals?

_We'll trade away other things to get these._

We prioritize:

- Preserving qmail's hard-earned security properties
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


## What are notqmail's non-goals?

_We'll trade very little of these to get other things._

We wish to avoid:

- Breaking compatibility
- Breaking existing features of the architecture
- Breaking your patches more than necessary
- Modifying or replacing core components

Given the reasons qmail is valuable to us, the cost of a change that exhibits any of the preceding non-goals is high. Proposing one such change will require unusually strong justification, documentation, testing, and design. For the community to accept such a change, the risk must be demonstrably _very_ low and the benefit _very_ high.
