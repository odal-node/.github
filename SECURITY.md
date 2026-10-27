# Security policy

This is the coordinated vulnerability disclosure policy for Odal Node. The contact
for reports is **security@odal-node.io**.

It is the organization-wide default. It applies to every repository under
[github.com/odal-node](https://github.com/odal-node) that does not publish its own
`SECURITY.md`. Where a repository has its own, that file applies instead.

## Report a vulnerability

**Do not open a public issue.** Report privately, either:

- through **Report a vulnerability** on the repository's **Security** tab, where it
  is enabled. This is preferred: the report, the advisory and the fix stay together.
- or by email to **security@odal-node.io**.

Include:

1. What the vulnerability is and what it allows.
2. Steps to reproduce, or a minimal proof of concept.
3. The affected repository, component and version. A commit SHA is best.
4. A suggested fix or mitigation, if you have one.

## Response times

| Step | Target |
|---|---|
| Acknowledgement | 48 hours |
| Initial assessment and severity | 5 business days |
| Fix or mitigation, critical or high severity | 14 days |
| Fix or mitigation, medium or low severity | 30 days |
| Public disclosure | After the fix is released, coordinated with you |

We follow coordinated disclosure as described by the
[OpenSSF Vulnerability Disclosure Working Group](https://github.com/ossf/wg-vulnerability-disclosures)
and agree timing and credit with you.

The project is pre-production and has one maintainer. These are targets, not a
staffed on-call rotation. If a critical report gets no acknowledgement within 48
hours, send it again: it was missed.

## Supported versions

Security fixes go into the **latest release** of the affected repository. After a new
minor version, the previous minor version receives security fixes for **90 days**.

Current releases are on each repository's **Releases** page and, for published
crates, on **crates.io**.

## Publication

- **After a fix ships, the vulnerability is published** as a GitHub Security Advisory
  on the affected repository and in its `CHANGELOG.md`: what it is, the affected
  versions, the impact, and what an operator has to do.
- **Publication may be delayed** while operators need time to apply a patch. The
  delay is never open-ended, and you are told the reason and the planned date.
- **Dependency advisories are scanned daily**, by a scheduled workflow, because a new
  advisory against an existing dependency changes nothing in the repository and would
  trigger nothing on its own. A repository without that workflow has a gap, not an
  exemption.

## Out of scope

- **Feature requests and ordinary bugs.** Use the repository's issue tracker.
- **Vulnerabilities in upstream dependencies.** Report them to the dependency's
  maintainers and to [RustSec](https://rustsec.org/). CI checks advisories with
  `cargo audit`, and we release a patched version once an upstream fix exists.
- **Deployments we do not operate.** Every node runs on its operator's own
  infrastructure. `odal-node.io` and `docs.odal-node.io` are static sites with no
  passport data and no production service. A finding against a self-hosted node
  belongs to whoever runs it, but if our code causes it, report it here.

## Highest-severity findings

- Leaked key material, weak randomness, or key material in a log or error body.
- Signature bypass or forgery: a passport accepted as signed by a key that did not
  sign it.
- **Audience escalation:** a caller reading data above its disclosure class. This has
  regulatory consequences for the operator.
- Schema or rule validation bypass that lets a non-compliant passport be published.
- Escape from the Wasm plugin sandbox.
- Transfer-chain integrity violations: skipped states or forged history.

## Credit

Reporters are credited in the CHANGELOG and release notes unless they prefer to stay
anonymous. **There is no bug bounty.** Unsolicited offers of paid fixes, and demands
for payment, get no reply.
