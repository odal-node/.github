# Contributing

This is the **organization-wide default** for Odal Node. It covers what is true in every
repository under [github.com/odal-node](https://github.com/odal-node).

**`dpp-core` and `dpp-engine` publish their own `CONTRIBUTING.md`.** Those files govern
in those repositories — read them instead, because they carry the build commands, the
crate layout and the dependency rules that this file cannot.

## Before you write code

**Open an issue first for anything beyond a typo.** Not as a formality: this project
encodes EU regulation, and a change that looks like a clean refactor can move a
regulatory claim to a place where it is no longer checkable. A short issue costs you ten
minutes and can save a rewrite.

For a change that touches a regulatory constant, a threshold, a date, a product scope or
a disclosure class, say in the issue **which primary source you read**. Not a blog post,
not a summary, not a secondary tracker — the Official Journal text, the standard, or the
regulator's own published guidance. A claim without a source you personally read will
not be merged, however plausible it is.

## Commits

[Conventional Commits](https://www.conventionalcommits.org/) v1.0.0:

```
<type>(<scope>): <subject>
```

- **Types:** `feat`, `fix`, `chore`, `docs`, `refactor`, `test`, `perf`, `security`
- **Subject:** imperative, under 50 characters — "add fix", not "added fix".
- **Breaking changes:** `!` after the scope — `feat(domain)!: remove deprecated field`.
- **Scope** is the functional area touched, never the repository's own name.

**Never include AI attribution**, `Co-Authored-By` trailers naming a tool, or generated
sign-offs. Use of a tool is not a fact about the change.

### Sign-off

Commits must be signed off under the
[Developer Certificate of Origin v1.1](https://developercertificate.org/):

```bash
git commit -s -m "fix(resolver): reject a malformed Digital Link path"
```

By signing off you certify you wrote the contribution, or have the right to submit it
under that repository's licence. CI rejects commits without the line.

**Note the licences differ.** `dpp-core` and `xml-sec` are Apache-2.0. `dpp-engine` is
BSL-1.1. Contributing to the engine means contributing to a source-available project
that converts to an open licence on its change date — read its `LICENSE` before you
start, not after.

## Pull requests

- Every change goes through a pull request. No direct pushes to `main`.
- The PR title is a Conventional Commit: it becomes the squash subject and cannot be
  corrected once a release is cut from it.
- All CI checks pass before review is requested. Green CI is the entry condition, not
  the goal.
- A new dependency needs a sentence in the description saying why. A new *direct*
  dependency in a published crate needs a paragraph.
- Branch names mirror the commit type: `feat/…`, `fix/…`, `docs/…`, `chore/…`.

**Do not leave work stubbed, `TODO`-ed, or deferred to "a follow-up" in a PR you have
marked ready.** Open it as a draft instead.

## What will get a change rejected

- **A regulatory claim with no source**, or a source that is a secondary summary.
- **A plan written as an accomplishment.** "Validates X" when it does not yet. If you are
  describing intent, use the future tense and say what condition would make it true.
- **A hardcoded version, date or deadline in a document.** Those go stale silently. Point
  at the place that owns the fact.
- **Anything that widens what a caller can read.** Disclosure classes are the one place
  where a permissive default has regulatory consequences for an operator.
- **Secrets, credentials, keystores or `.env` files in the diff**, including in a test
  fixture. A leak cannot be un-pushed.
- **A real company's name in a test fixture.** It implies a relationship that may not
  exist.

## Security

Do not report a vulnerability in a pull request or a public issue — that publishes it.
See [SECURITY.md](SECURITY.md).

## Conduct

[CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) applies to every interaction in these
repositories.
