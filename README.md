# .github

Organization-level files for [github.com/odal-node](https://github.com/odal-node).

Nothing here is code. Two distinct jobs live in this repository, and they behave
differently — do not confuse them.

## 1. The organization profile page

`profile/README.md` renders at **https://github.com/odal-node**. It is the most-read
and least-reviewed page in the organization: a visitor sees it before any repository,
and every change to it is published the moment it is pushed.

Four rules for editing it:

- **It is a signpost, not a document.** One screen plus the routing table. If a reader
  learns nothing new after clicking through to `dpp-core`, the page has done its job.
  Restating a repository README here gives crawlers two competing canonical descriptions
  of the same project.
- **No dated regulatory claims.** No mandate dates, effective dates, thresholds or
  standard numbers. Those have a home in `dpp-core`'s instrument manifests and go stale
  the moment they are copied. Link out; do not restate.
- **No non-public repository may be named here**, and no claim may be made about users,
  pilots, partners or revenue that is not verifiably true today. The commercial section
  describes a *capability* being built — never a repository, a date, or a price.
- **Every link is checked before the page is pushed.** A signpost that points at a 404
  is worse than no signpost. The landing site routes fewer pages than its source tree
  suggests: files prefixed `_` are not built.

The commercial paragraph follows the pattern used by open-core projects that keep their
credibility — state the self-host grant first and unconditionally, name the managed
option in one sentence, say plainly which part is closed and why, and point at a real
call to action rather than a promised date. Grafana's profile acknowledges a closed part
in a single clause without enumerating it; n8n's offers the cloud option in one line
next to the self-host docs. Both are the shape to copy. The Catena-X association's
profile, which lists private repositories by name, is the shape to avoid here — that is
a consortium telling its members where things are, and our publication rules forbid it.

## 2. Default community health files

`SECURITY.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SUPPORT.md` and the templates
under `.github/` are **defaults**. GitHub applies each one to any repository in the
organization that does not carry its own copy of that file.

| File | Applies to | Overridden by |
|---|---|---|
| `SECURITY.md` | dpp-web, xml-sec | dpp-core, dpp-engine (own copies) |
| `CONTRIBUTING.md` | dpp-web, xml-sec | dpp-core, dpp-engine (own copies) |
| `CODE_OF_CONDUCT.md` | every repository | — (no repository carries one) |
| `SUPPORT.md` | every repository | — |
| `.github/ISSUE_TEMPLATE/config.yml` | dpp-web | dpp-core, dpp-engine (own copies) |
| `.github/pull_request_template.md` | dpp-web, xml-sec | dpp-core, dpp-engine (own copies) |

**`xml-sec` is a fork of someone else's project and inherits these defaults by
accident, not by intent.** It carries no health files of its own, so our
`CONTRIBUTING.md` and `CODE_OF_CONDUCT.md` would govern a repository whose real home is
[structured-world/xml-sec](https://github.com/structured-world/xml-sec) — telling a
contributor to open a pull request here when it belongs upstream. Give the fork its own
one-paragraph `CONTRIBUTING.md` redirecting upstream, or accept that the defaults
misdirect. It already carries upstream's `FUNDING.yml`, which is correct and should stay.

Two consequences that are easy to get wrong:

- **A default is a promise made on behalf of every repository that inherits it.** Adding
  `SECURITY.md` here commits `security@odal-node.io` to answering reports about
  repositories whose security posture nobody has reviewed. Widen the promise
  deliberately, or give the repository its own narrower policy.
- **`blank_issues_enabled: false` in a default `config.yml` disables blank issues in
  every inheriting repository, including ones that have no issue forms to offer
  instead.** That leaves a repository with no way to file an issue at all. The default
  here deliberately leaves blank issues enabled; only a repository that ships its own
  forms should turn them off.

Default files are not copied into clones or downloads of the repositories that inherit
them. They resolve at read time on github.com only.

## Not here

- **No `LICENSE`.** These are organization policy documents. Nobody should reuse them
  verbatim, and the default — all rights reserved — is the correct outcome.
- **No `FUNDING.yml`.** There is no entity yet to route sponsorship to.
