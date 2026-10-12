<p align="center">
  <img alt="GOVP — Sign once. Verify anywhere. Open protocol, local verification, no central API." src="https://raw.githubusercontent.com/govp-protocol/govp/main/brand/govp-org-header.svg" width="100%">
</p>

<p align="center"><strong>Open protocol stewarded by Gemacode.</strong></p>

GOVP makes files and digital artifacts independently verifiable without an
account, a central API or a proprietary verifier.

A publisher places a small, signed GOVP record next to a document, dataset,
model or build artifact. Anyone can then verify the record and the exact
artifact bytes locally with an open implementation.

[Try the browser verifier](https://govp.io/govp/verify.html) ·
[Read the documentation](https://govp.io/govp/docs.html) ·
[Implement GOVP-1](https://github.com/govp-protocol/govp/blob/main/spec/GOVP-1.txt) ·
[View the source](https://github.com/govp-protocol/govp)

<p align="center">
  <img alt="Sign a portable GOVP record, distribute it beside an artifact, then verify both locally." src="https://raw.githubusercontent.com/govp-protocol/govp/main/brand/govp-flow.svg" width="100%">
</p>

## The problem GOVP solves

Digital artifacts routinely leave the systems that created them. They are
downloaded, mirrored, emailed, archived and processed by other software.

- A checksum detects changed bytes, but does not carry a signature.
- A raw signature does not define a shared record format, identifier or
  canonical signing input.
- A hosted verification API works only while its account, service and trust
  boundary remain available.

GOVP standardizes the small layer between those primitives: a readable signed
record, deterministic verification rules, content-derived identifiers, JSON
Schema and byte-exact conformance vectors.

## Verify a signed artifact in 60 seconds

```bash
python -m pip install govp==0.1.13
govp examples --extract govp-examples
govp verify govp-examples/manufacturing-record.govp.txt \
  --asset govp-examples/manufacturing-record.statement.txt
```

```text
GOVP verification: VALID
  format       pass
  signature    pass
  govp-id      pass
  canonical    not checked
  asset        pass
  record       GOVP-DOC-cb352d4b8a77
```

The example is synthetic. Verification runs locally and sends neither the
record nor the artifact to GOVP.

## Change one line. Watch GOVP reject it.

The same repository includes a copy of the artifact with one modified line.
Its signed GOVP record is still authentic, but the supplied artifact no longer
matches the SHA-256 digest inside that record.

<p align="center">
  <img alt="The original synthetic artifact passes GOVP verification while a one-line modification fails the asset SHA-256 check." src="https://raw.githubusercontent.com/govp-protocol/govp/main/brand/govp-integrity-demo.svg" width="100%">
</p>

```bash
govp verify examples/manufacturing-record.govp.txt \
  --asset examples/manufacturing-record.tampered.statement.txt
```

```text
GOVP verification: INVALID
  format       pass
  signature    pass
  govp-id      pass
  canonical    not checked
  asset        FAIL
  record       GOVP-DOC-cb352d4b8a77
```

`signature pass` proves the record itself was not forged. `asset FAIL` proves
the supplied bytes are not the exact artifact that record describes. The
command exits with status `1`, so the same verification can gate a release or
CI workflow.

## What a valid result means

GOVP can establish that the record was signed by its included public key, that
its identifier is internally consistent and that supplied artifact bytes match
the signed SHA-256 digest. Remote verification can also bind the final HTTPS
location to the signed canonical URL.

GOVP does **not** decide whether a statement is true, certify the legal identity
behind a key or create an independent timestamp. The optional GOVP-STATUS-1
extension adds same-origin key lifecycle and record revocation; those results
remain separate from offline core validity and application policy.

## Built for artifacts that travel

| Example | What GOVP keeps verifiable |
|---|---|
| Published documents | The exact statement, policy or report bytes |
| Datasets and models | A frozen snapshot used for analysis or evaluation |
| Software releases | A build artifact after download, mirroring or archival |
| Benchmarks and results | The precise result set associated with a declaration |
| Operational records | A portable signed record outside the originating system |

## Compose GOVP with the evidence stack you already use

GOVP is not a replacement for signing, attestation or transparency systems.
It provides a portable binding to their exact output bytes:

- SCITT signed statements and transparency receipts;
- COSE messages and DSSE envelopes;
- in-toto attestations and bundles;
- Sigstore bundles; and
- Verifiable Credentials or C2PA objects when those models supply the claims,
  identity or provenance layer.

Each upstream object still requires its native verifier and policy. GOVP proves
that the supplied bytes match the portable signed GOVP record; it does not
silently inherit the upstream system's identity, transparency or attestation
guarantees.

Read [Composing GOVP with evidence ecosystems](https://github.com/govp-protocol/govp/blob/main/docs/composition.md)
for the layered verification model and primary specifications.

## Open protocol building blocks

| Repository | Responsibility | License |
|---|---|---|
| [`govp`](https://github.com/govp-protocol/govp) | GOVP-1 specification, schemas, conformance vectors and Python reference verifier 0.1.13 | Apache-2.0 |
| [`govp-js`](https://github.com/govp-protocol/govp-js) | Independent Node/browser verifier [`@govp/verifier` 0.1.11](https://www.npmjs.com/package/@govp/verifier/v/0.1.11) | Apache-2.0 |
| [`govp.io`](https://github.com/govp-protocol/govp.io) | Documentation, normative publication and local browser verifier | MIT |

The protocol is not tied to Python or JavaScript. Its wire behavior is defined
by the normative text and conformance vectors. Independent Go, Rust, Java and
other implementations are welcome.

GOVP-1 is frozen. Low protocol churn is a compatibility guarantee by design;
implementation, conformance, security and documentation work remains active.

## Build with us

Good first contributions include:

- an independent implementation or conformance report;
- a new synthetic interoperability vector;
- a specification ambiguity found while implementing;
- integration guidance for a language, build system or artifact workflow.

[Implementation guide](https://github.com/govp-protocol/govp/blob/main/docs/conformance.md) ·
[Contributing](https://github.com/govp-protocol/govp/blob/main/CONTRIBUTING.md) ·
[Report a specification ambiguity](https://github.com/govp-protocol/govp/issues/new?template=spec-ambiguity.yml) ·
[Propose an implementation](https://github.com/govp-protocol/govp/issues/new?template=implementation.yml)

## Stewardship

GOVP is stewarded by Gemacode, a brand of Brilyetz Holding S.L. The public
GitHub organization is protocol-only: hosted products, customer systems and
commercial extensions are outside its scope.

The canonical GOVP visual identity and its usage rules are maintained in the
[`govp/brand`](https://github.com/govp-protocol/govp/tree/main/brand)
directory.

Security reports should use
[private vulnerability reporting](https://github.com/govp-protocol/govp/security/advisories/new)
or be sent to [`research@gemacode.org`](mailto:research@gemacode.org).
