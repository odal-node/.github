# .github

Organization-level files for [github.com/odal-node](https://github.com/odal-node).
Nothing here is code. The repository does two separate jobs.

## 1. The organization profile

`profile/README.md` renders at **https://github.com/odal-node**. Visitors see it before
any repository, and a change goes live the moment it is pushed.

Rules for editing it:

- **Keep it a signpost.** What the project is, the licence split, the status, how the
  pieces fit, and links. Do not restate a repository README; search engines would see
  two competing descriptions of the same project.
- **No dated regulatory claims.** No mandate dates, thresholds or standard numbers.
  They live in `dpp-core`'s instrument catalog and go stale when copied.
- **Public facts only.** Name no non-public repository. Make no claim about users,
  pilots, partners or revenue that is not verifiable today. Describe commercial plans
  as a capability and a roadmap status, never a date or a price.
- **Check every link before pushing.** On the landing site, source files prefixed `_`
  are not built, so a page that exists in the source tree can still be a 404.

All documentation in the organization follows [DOCS-STYLE.md](DOCS-STYLE.md).

## 2. Default community health files

`SECURITY.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SUPPORT.md`, `GOVERNANCE.md`
and the templates under `.github/` are **defaults**. GitHub applies each one to any
repository in the organization that does not have its own copy.

| File | Applies to | Overridden in |
|---|---|---|
| `SECURITY.md` | dpp-web | dpp-core, dpp-engine |
| `CONTRIBUTING.md` | dpp-web | dpp-core, dpp-engine |
| `GOVERNANCE.md` | dpp-web | dpp-core, dpp-engine |
| `CODE_OF_CONDUCT.md` | every repository | none |
| `SUPPORT.md` | every repository | none |
| `.github/ISSUE_TEMPLATE/config.yml` | dpp-web | dpp-core, dpp-engine |
| `.github/pull_request_template.md` | no repository today | dpp-core, dpp-engine, dpp-web |

Things that are easy to get wrong:

- **A default makes a promise for every repository that inherits it.** This
  `SECURITY.md` commits `security@odal-node.io` to handling reports for repositories
  nobody has reviewed for security. Widen that deliberately, or give a repository its
  own narrower policy.
- **`blank_issues_enabled: false` in the default `config.yml` would disable blank
  issues everywhere it is inherited,** including repositories with no issue forms. They
  would have no way to file an issue. Only a repository that ships its own forms
  should turn blank issues off.
- **A fork of someone else's project inherits these defaults too.** Our
  `CONTRIBUTING.md` would send its contributors here instead of upstream. Give a live
  fork its own `CONTRIBUTING.md` that points upstream, and archive it once nothing
  depends on it. The `xml-sec` fork is archived: the engine uses the upstream crate,
  [structured-world/xml-sec](https://github.com/structured-world/xml-sec), from
  crates.io.

Default files are resolved on github.com when read. They are not copied into clones or
downloads of the repositories that inherit them.

## Not here

- **No `LICENSE`.** These are organization policy documents, not reusable text, so the
  default (all rights reserved) is the intended outcome.
- **No `FUNDING.yml`.** There is no entity to receive sponsorship yet.
