# Odal Node

Self-hosted software for issuing, signing and serving EU Digital Product Passports
(DPPs), written in Rust.

`dpp-core` is an open-source Rust library under Apache-2.0: stateless, with no
database and no network I/O. `dpp-engine` is the self-hostable node built on it,
under the Business Source License 1.1. Running it in production for your own
organisation's products and compliance obligations is free. Offering it to third
parties as a hosted service, or embedding it in a competing product, needs a
commercial licence.

> [!NOTE]
> **Status: pre-production.** CI runs the full passport lifecycle against
> PostgreSQL on every change, but no operator runs a node against real product
> data yet. APIs and schemas still change between minor versions.

## Repositories

| Repository | Licence | What it is |
|---|---|---|
| [**dpp-core**](https://github.com/odal-node/dpp-core) | Apache-2.0 | Rust crates on [crates.io](https://crates.io/crates/dpp-domain): the passport data model, versioned JSON Schemas per product group, regulatory validation rules, Ed25519/JWS signing, W3C Verifiable Credentials, product identifiers and their digital links (GS1 Digital Link, identification link, DID), Asset Administration Shell export, and EU registry types. |
| [**dpp-engine**](https://github.com/odal-node/dpp-engine) | BSL-1.1 | The node: an Axum HTTP API over PostgreSQL, `did:web` signing identity, a public resolver for each passport's digital link, a wasmtime sandbox for product group plugins, CSV/XLSX bulk import, and the `odal` CLI. |
| [**dpp-web**](https://github.com/odal-node/dpp-web) | Apache-2.0 | The sites: [odal-node.io](https://odal-node.io) and [docs.odal-node.io](https://docs.odal-node.io). |

## How the pieces fit

```mermaid
flowchart LR
    subgraph oss["Open source, on crates.io"]
        core["dpp-core<br/>model, schemas, rules,<br/>signing, identifiers"]
    end

    subgraph own["Your systems"]
        erp["ERP, PLM or scripts<br/>REST API, webhooks"]
        sheets["Spreadsheets<br/>bulk import"]
        cli["odal CLI"]
    end

    subgraph infra["Your infrastructure"]
        node["dpp-node<br/>validate, sign, publish,<br/>lifecycle, audit trail"]
        plugins["Product group plugins<br/>Wasm sandbox"]
        keys[("Signing key")]
        pg[("PostgreSQL")]
        resolver["dpp-resolver<br/>public, read-only"]
    end

    subgraph world["Outside your network"]
        scan["Anyone scanning the code<br/>reads the public view"]
        holder["Repairers, recyclers<br/>read restricted parts<br/>with a credential"]
        verifier["Verifiers fetch your<br/>did:web document"]
        supplier["Suppliers' passports<br/>pinned as components"]
        registry["EU DPP registry<br/>receives registrations"]
        backup["Independent provider<br/>holds a back-up copy"]
    end

    core --> node & resolver & plugins
    erp <--> node
    sheets --> node
    cli --> node
    node --- plugins & keys & pg
    node --> resolver --> scan
    node --> holder & verifier
    node --- supplier
    node -.-> registry & backup
```

Everything in the middle box runs on your infrastructure. Odal operates none of it
and receives none of its data. Both binaries compile `dpp-core` in, and product group
plugins are written against its plugin SDK.

- **Your systems** talk to the node over its REST API with an API key, or import
  spreadsheets in bulk. The node calls them back with a signed webhook whenever a
  passport changes.
- **The digital link** on the product opens the passport at your resolver: a GS1
  Digital Link when the product has a GTIN, otherwise the passport's own address. The
  resolver only ever serves the public view.
- **Restricted parts** of a passport are read from the node with an access credential
  that names the reader's role.
- **Signatures** are made with your key and verify against your public `did:web`
  document, without contacting Odal.
- **Component passports** can live on other companies' nodes. A passport pins the
  hash of each component's signed public view, and the node fetches the components
  down the bill of materials and checks every pin.
- **Dotted lines** need configuration. The EU registry connection queues every
  registration but submits nothing until registry credentials are set, and then only
  to the registry's sandbox. The back-up copy needs object storage held by an
  independent provider.

## Why self-host

- **Your data stays with you.** Product, supplier and bill-of-materials data is
  stored in your own PostgreSQL. Odal never receives it. What leaves your network is
  what you configure or the law requires: the public passport view, the restricted
  parts a credential holder may read, the EU registry submission, and the independent
  back-up copy.
- **No lock-in.** The data model, schemas and validation rules are Apache-2.0.
  Passports are signed with your key and verify without any Odal service.
- **One node per company.** One database, one signing key, nothing shared with
  another operator.

## Get started

- **Use the library:** `cargo add dpp-domain`, then the
  [dpp-core quick start](https://github.com/odal-node/dpp-core#quick-start).
- **Run a node:** the [dpp-engine quick start](https://github.com/odal-node/dpp-engine#quick-start)
  takes you from `git clone` to a published, resolvable passport.
- **Read the docs:** [docs.odal-node.io](https://docs.odal-node.io), including the
  [API reference](https://docs.odal-node.io/api/).

Managed operation (a node run for you, still one node per company) is under
consideration and not offered. It is listed on the
[roadmap](https://odal-node.io/roadmap/) with everything else that is planned or
being built.

## Questions and contributions

Ask in Discussions on [dpp-core](https://github.com/odal-node/dpp-core/discussions) or
[dpp-engine](https://github.com/odal-node/dpp-engine/discussions); public answers help
the next person too. [SUPPORT.md](https://github.com/odal-node/.github/blob/main/SUPPORT.md)
lists where each kind of question goes, and
[CONTRIBUTING.md](https://github.com/odal-node/.github/blob/main/CONTRIBUTING.md)
covers commits and pull requests.

The most useful report is a place where the software disagrees with EU law, with
the text you read it against.

## Security

Report vulnerabilities privately to **security@odal-node.io** or through the
repository's **Report a vulnerability** button, never in a public issue. Policy:
[SECURITY.md](https://github.com/odal-node/.github/blob/main/SECURITY.md).

## Credits

Odal Node builds on other people's open-source work and is tested against it.
[CREDITS.md](https://github.com/odal-node/.github/blob/main/CREDITS.md) names those
projects and what each one does here: upstream maintainers who fixed what we
reported, the reference implementations `dpp-core` is tested against, and the
single-maintainer libraries in the signing and validation path.
