# Documentation style guide

How Odal Node writes documentation: repository READMEs, `docs/` folders, crate
READMEs published to crates.io, and [docs.odal-node.io](https://docs.odal-node.io).
It applies to every public repository in the organization.

## Audience and voice

Write for an engineer who is evaluating, integrating or operating the software.
Write as a peer: direct, specific, plain.

- **Show, then explain.** Put the command, the request or the code first, and the
  reasoning after it.
- **Describe mechanisms, not virtues.** Write "the node refuses to start when a
  required adapter is a stub", not "the node cannot lie about its trust level".
- **One fact, one home.** Versions, dates, counts, route lists and environment
  variables already live in code or in a generated file. Link to that source
  instead of copying it into prose, where it goes stale without failing a test.
- **Say what is not done.** Use the status labels below. Planned work is never
  written in the present tense.

## Page structure

A repository README follows this order:

1. **Title and summary.** Sentence one says what the repository is and its licence.
2. **Status.** One line a reader must see before depending on the code.
3. **Quick start.** The shortest path to a working result: copy-pasteable commands,
   then the expected output. Aim for five minutes on a machine that already has the
   prerequisites. When a step takes longer (a first build), say how long.
4. **How it works.** One diagram and a short description of the moving parts.
5. **Reference.** Links to the API, configuration, CLI and deeper documents.
6. **Background.** Regulatory context and design rationale come last.

docs.odal-node.io sorts pages by what the reader is doing, following
[Diátaxis](https://diataxis.fr/):

| Kind | The reader is | Example |
|---|---|---|
| Tutorial | learning by doing | Quick start |
| How-to guide | completing a task | Importing product data |
| Reference | looking something up | Configuration reference, API reference |
| Explanation | building understanding | How the node works, Regulatory context |

Keep the kinds apart. A how-to guide links to the explanation instead of
containing it.

## Words

| Avoid | Write instead |
|---|---|
| "honest", "honesty", "truth", "lie", "promise" (about software behaviour) | The mechanism: "fail-fast startup validation", "the response names the adapter in use" |
| "golden rule", "the point", "proposition", "manifesto", "philosophy" | State the rule |
| "ghost" for an adapter, outside a code literal | "stub adapter". Quote `ghost` only where it is the literal value an API or metric returns |
| "sovereign" as an adjective for software | "self-hosted", "runs on your infrastructure" |
| "seamless", "simply", "just", "easy", "powerful", "robust", "blazing", "world-class" | Delete it, or give the number |
| "not X, but Y" used for emphasis | State Y |
| "we believe", "we think" | The decision and its reason |

Emoji are not used as markers in prose. For a warning, use a GitHub alert
(`> [!WARNING]`) in Markdown and `<Aside type="caution">` on the docs site.

Spelling is British English (organisation, behaviour, licence as the noun),
matching the documentation site. Proper names keep their own spelling: Apache
License 2.0, Business Source License 1.1, the `LICENSE` file.

## Punctuation and formatting

- **No em dashes (—) and no double hyphens (--) in prose.** Use a comma, a colon,
  parentheses or two sentences. En dashes stay in number and date ranges
  (2027–2030). Code is not prose: a flag such as `--release`, and program output
  quoted exactly as the software prints it, keep their characters.
- **Headings** use sentence case and name what the section contains.
- **Code blocks** carry a language tag (`bash`, `rust`, `json`, `http`). Commands
  are copy-pasteable: no `$` prompt and no output inside the command block. Put
  expected output in a separate block.
- **Placeholders** are written `<like-this>`.
- **Tables** hold comparisons and reference data. Reasoning goes in prose.
- **Diagrams** are [Mermaid](https://mermaid.js.org/), so they are diffable and
  render on GitHub.

## The licence statement

Use this wording where both repositories are described: the organization profile,
the engine README and the documentation site.

> `dpp-core` is an open-source Rust library under Apache-2.0: stateless, with no
> database and no network I/O. `dpp-engine` is the self-hostable node built on it,
> under the Business Source License 1.1. Running it in production for your own
> organisation's products and compliance obligations is free. Offering it to third
> parties as a hosted service, or embedding it in a competing product, needs a
> commercial licence.

`dpp-core`'s own pages state only its own licence. A published library does not
name its consumers, and `crates/dpp-tests/tests/publication_boundary.rs` fails if
it does.

## Status labels

The same five labels as the public roadmap:

| Label | Meaning |
|---|---|
| Available | On `main`, tested, usable today |
| Built, waiting on a legal step | Implemented, but it cannot have legal effect until an outside condition is met |
| In progress | Being built now |
| Planned | Committed to, not started |
| Considered | Under evaluation, no commitment |

The project as a whole is **pre-production**: no production deployments and no
external users. Every front door says so.

## Regulatory and standards text

- Cite EU acts by number and article: "Regulation (EU) 2023/1542, Art. 77(2)".
  Official Journal text may be quoted.
- **Never quote a CEN, CENELEC or ISO standard** (EN 18219, EN 18221 and others).
  They are sold per reader. Cite the clause and describe what it requires in your
  own words.
- Regulatory dates live in code (the instrument catalog in `dpp-domain`). Prose
  links to them.

## Publication rules

- No non-public repository, internal path, decision-record number or planning
  identifier on a public surface.
- No claim about users, pilots, partners or revenue that is not verifiable today.

## Before you merge a documentation change

- [ ] Every command was run against the commit being documented.
- [ ] Every route, flag and environment variable was checked against the code:
      `odal <command> --help`, the OpenAPI bundle, `.env.example`.
- [ ] Each feature's status matches the roadmap.
- [ ] No em dash or double hyphen in prose:

```bash
grep -rn -e '—' -e ' -- ' --include='*.md' --include='*.mdx' .
```
