# Credits

Odal Node builds on other people's open-source work and is tested against it. This
page names the projects that do the most for it and what each one does here. Each
project keeps its own licence; see its repository.

A project is listed when it meets one of the three tests below, one per section.

## Upstream maintainers who fixed what we reported

| Project | Maintained by | Its role in Odal Node |
|---|---|---|
| [xml-sec](https://github.com/structured-world/xml-sec) | [@polaz](https://github.com/polaz) at [Structured World](https://github.com/structured-world) | A pure-Rust implementation of XMLDSig, XMLEnc and C14N. `dpp-engine` uses it to verify the signatures on EU Trusted Lists. |
| [eudi-lib-jvm-sdjwt-kt](https://github.com/eu-digital-identity-wallet/eudi-lib-jvm-sdjwt-kt) | [EU Digital Identity Wallet](https://github.com/eu-digital-identity-wallet) | One of two independent SD-JWT implementations `dpp-core` is tested against: it reads the SD-JWTs `dpp-core` issues, and `dpp-core` must read the ones it issues. |

## Reference implementations `dpp-core` is tested against

`dpp-core`'s CI runs its output through each of these, and through the EU SD-JWT
library above, on every push and pull request. None of them shares code with
`dpp-core`, so a misreading of a specification in our code has to get past an
implementation that read the specification separately.

| Project | Maintained by | What it checks |
|---|---|---|
| [DSS (Digital Signature Service)](https://github.com/esig/dss) | European Commission | Validates the JAdES signatures `dpp-core` produces and reports what each one is |
| [@sd-jwt/core](https://github.com/openwallet-foundation-labs/identity-common-ts) | OpenWallet Foundation Labs | The second independent SD-JWT implementation, tested in both directions like the first |
| [GS1 Barcode Syntax Engine](https://github.com/gs1/gs1-syntax-engine) | GS1 | Judges every GS1 Digital Link `dpp-core` builds against GS1's own syntax rules |
| [aas-core3.0](https://github.com/aas-core-works/aas-core3.0-python) | aas-core-works | Reads the Asset Administration Shell environments `dpp-core` exports |
| [aas-test-engines](https://github.com/admin-shell-io/aas-test-engines) | Industrial Digital Twin Association (IDTA) | Runs IDTA's own tests over the same environments |
| [pyld](https://github.com/digitalbazaar/pyld) | Digital Bazaar | Expands every JSON-LD context and document `dpp-core` emits, as an independent JSON-LD 1.1 processor |
| [DID Test Suite](https://github.com/w3c/did-test-suite) | W3C | Runs the DID documents `dpp-core` produces through the W3C's own tests |

## Single-maintainer libraries in the signing and validation path

Each is published by one maintainer and decides an outcome a passport depends on.

| Project | Maintained by | Its role in Odal Node |
|---|---|---|
| [serde_jcs](https://github.com/l1h3r/serde_jcs) | [@l1h3r](https://github.com/l1h3r) | RFC 8785 canonical JSON: the exact bytes behind every passport signature (`dpp-core`) |
| [jsonschema](https://github.com/Stranger6667/jsonschema) | [@Stranger6667](https://github.com/Stranger6667) | Validates every passport against its product group's JSON Schema (`dpp-core`) |
| [qrcode](https://github.com/kennytm/qrcode-rust) | [@kennytm](https://github.com/kennytm) | Renders the QR code printed on the product (`dpp-engine`) |
| [x509-verify](https://github.com/bhesh/x509-verify) | [@bhesh](https://github.com/bhesh) | Checks certificate-chain signatures when the node verifies an electronic seal (`dpp-engine`; sealing is experimental) |

Every other dependency is declared in its repository's manifest (`Cargo.toml` or `package.json`).
