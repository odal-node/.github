# Odal Node

Infrastructure for EU Digital Product Passports. An Apache-2.0 Rust standard library
anyone can build on, and a source-available node that issues, signs and serves
passports **on infrastructure you control** — not on ours.

> **Pre-production, in active development.** No operator is running this against real
> product data yet. Read the code before you depend on it.

## Start here

| | |
|---|---|
| **[dpp-core](https://github.com/odal-node/dpp-core)** | **The standard.** Domain types, Ed25519/JWS signing, W3C Verifiable Credentials, GS1 Digital Link, versioned JSON Schema validation. Stateless — no database, no HTTP framework, no infrastructure. **Apache-2.0.** |
| **[dpp-engine](https://github.com/odal-node/dpp-engine)** | **The node.** HTTP services, PostgreSQL persistence, sandboxed Wasm plugin host, public Digital Link resolver, and a command-line control plane. Built on dpp-core. **BSL-1.1 — self-hosting for your own compliance obligations is free.** |
| **[dpp-web](https://github.com/odal-node/dpp-web)** | The sites: [odal-node.io](https://odal-node.io) and [docs.odal-node.io](https://docs.odal-node.io). |

**Documentation → [docs.odal-node.io](https://docs.odal-node.io)**

## Where code goes

If something changes because an **EU regulation** changed, it belongs in `dpp-core`.
If it changes because of **how a system is deployed, run or operated**, it belongs in
`dpp-engine`.

That split is the point, not an implementation detail. It is what lets the regulatory
half stay Apache-2.0 and be vendored by anyone — including people who will never run
our node.

## Self-hosted first. Managed operation is coming.

**Everything needed to run a node yourself is in these repositories and stays there.**
The engine's free self-host grant is a licence term, not a trial tier.

Not every obligated company wants to operate one. **Managed operation — we run the
node, you keep it** — is being built now and is not yet open. The provisioning and
fleet-operation tooling behind it is closed and will stay closed: it is the commercial
half of an open-core project, and the reason the rest can be given away.

It changes nothing about the isolation model, which is already settled: **one operator,
one node, one database, one key, and no shared data paths at any layer.** A shared
endpoint holding everyone's passports would invert the whole proposition. What is still
open is only how the machines get provisioned.

**[Join the waitlist →](https://odal-node.io/waitlist)**

## Upstream

`dpp-engine` verifies EU Trusted List signatures with
[**xml-sec**](https://github.com/structured-world/xml-sec) — pure-Rust XMLDSig, XMLEnc
and C14N, written by [**@polaz**](https://github.com/polaz) at
[Structured World](https://github.com/structured-world) and published under Apache-2.0.
Our [fork](https://github.com/odal-node/xml-sec) exists only to carry one patch while
[structured-world/xml-sec#158](https://github.com/structured-world/xml-sec/issues/158)
is open. It is their project, not ours.

## Questions and contributions

Ask in Discussions on [dpp-core](https://github.com/odal-node/dpp-core/discussions) or
[dpp-engine](https://github.com/odal-node/dpp-engine/discussions) rather than by email
where you can — an answer in public is read many times.
[SUPPORT.md](https://github.com/odal-node/.github/blob/main/SUPPORT.md) covers what makes
a question answerable and what this project cannot advise on;
[CONTRIBUTING.md](https://github.com/odal-node/.github/blob/main/CONTRIBUTING.md) covers
commits, sign-off, and what gets a change rejected.

The most valuable report we can receive is **"the software is wrong about EU law, and
here is the text I read it against."**

## Security

Report vulnerabilities privately to **security@odal-node.io**. Never in a public issue.
Full policy: [SECURITY.md](https://github.com/odal-node/.github/blob/main/SECURITY.md)
