# Security Policy

**This is the coordinated vulnerability disclosure (CVD) policy for Odal Node, and
`security@odal-node.io` is the single point of contact for reporting vulnerabilities.**

It is the **organization-wide default**: it applies to any repository under
[github.com/odal-node](https://github.com/odal-node) that does not publish its own
`SECURITY.md`. Where a repository does publish one, that file governs and this one does
not apply to it.

## Reporting a vulnerability

**Do not open a public issue for a security vulnerability.**

Report privately to **security@odal-node.io** with:

1. A description of the vulnerability and its potential impact.
2. Steps to reproduce, or a minimal proof of concept.
3. The affected repository, component and version — a commit SHA is ideal.
4. Any suggested fix or mitigation, if you have one.

Where GitHub private vulnerability reporting is enabled on the repository, the
**Report a vulnerability** button on its Security tab is equally acceptable and is
preferred, because it keeps the report, the advisory and the fix in one place.

## What to expect

| Step | Timeframe |
|---|---|
| Acknowledgement of your report | Within 48 hours |
| Initial assessment and severity classification | Within 5 business days |
| Fix or mitigation for critical/high severity | Within 14 days |
| Fix or mitigation for medium/low severity | Within 30 days |
| Public disclosure, coordinated with you | After a fix is released |

We follow coordinated vulnerability disclosure as recommended by the
[OpenSSF Vulnerability Disclosure Working Group](https://github.com/ossf/wg-vulnerability-disclosures),
and will work with you on timing and credit.

**This project is pre-production and maintained by one person.** The timeframes above
are commitments we intend to meet, not a staffed on-call rotation. If a report is
critical and you have had no acknowledgement within 48 hours, send a second mail — it
was missed, not triaged.

## Supported versions

Security patches are issued for the **latest tagged release** of the affected
repository. When a new minor version is released, the previous minor continues to
receive security patches for **90 days**, after which support for it ends.

The current release of any repository is on its **Releases** page, and for published
crates on **crates.io**. This policy deliberately does not name a version number —
a version written into a policy document goes stale silently and has done so here
before.

## What we publish, and when

- **After a fix ships, the vulnerability is published** — as a GitHub Security Advisory
  on the affected repository and in that repository's `CHANGELOG.md`, with a description,
  the affected versions, the impact, and what an operator has to do. A fix released
  silently is a fix that only protects the people who happened to upgrade.
- **We may delay publication** where the risk of disclosing outweighs the benefit — for
  example while operators still need time to apply a patch. We do not delay it
  indefinitely, and the reporter is told the reason and the intended date.
- **Dependency advisories are scanned daily, not only on push.** An advisory published
  against a dependency that is already in the tree changes nothing in the repository, so
  nothing would trigger a run. Where that daily scan exists it is a scheduled workflow
  in the repository; where it does not yet, that is a gap and not a decision.

## Out of scope

- **Feature requests and non-security bugs.** Use the repository's issue tracker.
- **Vulnerabilities in upstream dependencies.** Report these to the dependency
  maintainer and to [RustSec](https://rustsec.org/). We monitor advisories via
  `cargo audit` in CI and will publish a patched release once a fix is available
  upstream. We cannot fix them ourselves, which is why they are out of scope for this
  policy rather than out of mind.
- **Findings against a deployment we do not operate.** Every Odal Node runs on its
  operator's own infrastructure; `odal-node.io` and `docs.odal-node.io` are static
  sites that host no passport data and no production service. A finding against a
  self-hosted node belongs to whoever runs it — though if it is caused by our code,
  we want to hear about it.

## What we consider severe

Across the organization's code, the findings that matter most are:

- Cryptographic key leakage, weak randomness, or key material reaching a log or an
  error body.
- Signature bypass or forgery — a passport accepted as authentic that was not signed
  by the key it claims.
- **Audience escalation**: any caller reading data above the disclosure class it is
  entitled to. This is the failure mode with regulatory consequences for an operator,
  not just for us.
- Schema or rule validation bypass that lets a non-compliant passport be issued as
  compliant.
- Sandbox escape from the Wasm plugin host.
- Transfer-chain integrity violations — skipped states, forged history.

## Recognition

We credit reporters in the CHANGELOG and release notes unless you prefer to stay
anonymous. **We do not operate a bug bounty programme and do not pay for reports.**
Unsolicited mail offering paid "fixes" or demanding payment for a disclosure will not
receive a reply.
