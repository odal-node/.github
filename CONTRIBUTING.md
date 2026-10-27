# Contributing

The organization-wide default for every repository under
[github.com/odal-node](https://github.com/odal-node).

`dpp-core` and `dpp-engine` publish their own `CONTRIBUTING.md` with build commands,
crate layout and dependency rules. In those repositories, read theirs.

## Before you write code

**Open an issue first for anything larger than a typo.** This code encodes EU
regulation, and a change that looks like a refactor can move a regulatory rule to a
place where no test checks it. A short issue up front is cheaper than a rewrite.

If the change touches a regulatory constant, threshold, date, product scope or
disclosure class, name the **primary source** you read in the issue: the Official
Journal text, the standard, or the regulator's own published guidance. A blog post,
summary or secondary tracker is not a source. Changes without a primary source are
not merged.

## Commits

Use [Conventional Commits](https://www.conventionalcommits.org/) v1.0.0:

```text
<type>(<scope>): <subject>
```

- **Types:** `feat`, `fix`, `docs`, `refactor`, `test`, `perf`, `chore`, `ci`, `build`, `style`, `revert`. In `dpp-core` and `dpp-engine`, CI rejects a pull request title with any other type.
- **Subject:** imperative mood, under 50 characters: "add fix", not "added fix".
- **Breaking change:** `!` after the scope, for example `feat(domain)!: remove deprecated field`.
- **Scope:** the functional area touched, never the repository's own name.
- **No AI attribution** and no `Co-Authored-By` trailer naming a tool.

### Sign-off

Sign off each commit under the
[Developer Certificate of Origin v1.1](https://developercertificate.org/):

```bash
git commit -s -m "fix(resolver): reject a malformed Digital Link path"
```

The sign-off certifies that you wrote the contribution, or have the right to submit
it under the repository's licence.

The licences differ between repositories. `dpp-core` and `dpp-web` are Apache-2.0.
`dpp-engine` is BSL-1.1: source-available, converting to Apache-2.0 four years after
each release. Read the repository's `LICENSE` before you start.

## Pull requests

- Every change goes through a pull request. Nobody pushes directly to `main`.
- The pull request title is a Conventional Commit. It becomes the squash commit
  subject and cannot be changed after a release is cut from it.
- CI passes before you request review.
- A new dependency needs one sentence in the description saying why. A new direct
  dependency of a published crate needs a paragraph.
- Branch names follow the commit type: `feat/…`, `fix/…`, `docs/…`, `chore/…`.
- Open unfinished work as a draft. A pull request marked ready has nothing stubbed,
  marked `TODO` or left for a follow-up.

Documentation changes follow the [documentation style guide](DOCS-STYLE.md).

## What gets a change rejected

- **A regulatory claim without a primary source.**
- **Planned behaviour described as current.** "Validates X" when it does not yet.
  Describe intent in the future tense and say what would make it true.
- **A version, date or deadline hard-coded into a document.** Link to the place that
  owns the value.
- **Anything that widens what a caller can read.** Disclosure classes are where a
  permissive default has regulatory consequences for an operator.
- **Secrets, credentials, keystores or `.env` files in the diff**, test fixtures
  included. A pushed secret is public.
- **A real company's name in a test fixture.** It implies a relationship that may not
  exist.

## Security

Do not report a vulnerability in a pull request or a public issue. See
[SECURITY.md](SECURITY.md).

## Conduct

[CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) applies to every interaction in these
repositories.
