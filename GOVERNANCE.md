# Governance

This is the **organization-wide default** for Odal Node. `dpp-core` and `dpp-engine`
publish their own `GOVERNANCE.md`, which governs in those repositories.

## Who decides

**Aleksandar Temelkov** is the sole maintainer and the sole organization owner. Every
decision — technical direction, what merges, what is released, what the licences are —
is made by one person.

This is stated plainly because the alternative is a document that implies a structure
which does not exist. There is no steering committee, no technical board, no vote, and
no appeals process. A contributor should know that before investing effort.

## What that means in practice

- **A proposal can be declined without a process.** You are owed a reason, and you will
  get one. You are not owed a vote.
- **There is a bus factor of one.** If this account is lost, the organization, its
  repositories and its billing go with it. This is a known, unresolved risk, not an
  oversight.
- **Nothing here is a foundation.** The project is not vendor-neutral and does not claim
  to be. `dpp-core` is Apache-2.0 precisely so that no one has to trust this governance
  structure to use it — the licence is the guarantee, not the org chart.

## The licence split is the real commitment

The regulatory layer is Apache-2.0 and stays that way. If this project stops, the
standard library it publishes remains usable, forkable and vendorable by anyone,
including competitors, with no further permission from anyone here. That is the
durable promise; this document is not.

`dpp-engine` is BSL-1.1: source-available, free to self-host for your own compliance
obligations, converting to an open licence on the change date stated in its `LICENSE`.
Read that file rather than any summary of it.

## How this changes

If the project gains maintainers, this document is rewritten before they are granted
merge rights, not after. A governance document that describes the previous shape of a
project is worse than none — it tells a contributor to expect something that no longer
holds.
