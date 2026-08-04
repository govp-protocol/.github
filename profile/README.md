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
git clone https://github.com/govp-protocol/govp.git
cd govp
python -m pip install .
govp verify examples/manufacturing-record.govp.txt \
  --asset examples/manufacturing-record.statement.txt
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

## What a valid result means

GOVP can establish that the record was signed by its included public key, that
its identifier is internally consistent and that supplied artifact bytes match
the signed SHA-256 digest. Remote verification can also bind the final HTTPS
location to the signed canonical URL.

GOVP does **not** decide whether a statement is true, certify the legal identity
behind a key, provide revocation or create an independent timestamp. Those are
separate trust and policy layers.

## Built for artifacts that travel

| Example | What GOVP keeps verifiable |
|---|---|
| Published documents | The exact statement, policy or report bytes |
| Datasets and models | A frozen snapshot used for analysis or evaluation |
| Software releases | A build artifact after download, mirroring or archival |
| Benchmarks and results | The precise result set associated with a declaration |
| Operational records | A portable signed record outside the originating system |

GOVP is intentionally narrower than Verifiable Credentials, C2PA and Sigstore.
The projects solve different trust problems and can be used together. See
[How GOVP fits](https://github.com/govp-protocol/govp/blob/main/docs/comparison.md)
for a neutral comparison and selection guide.

## Open protocol building blocks

| Repository | Responsibility | License |
|---|---|---|
| [`govp`](https://github.com/govp-protocol/govp) | GOVP-1 specification, schemas, conformance vectors and Python reference verifier | Apache-2.0 |
| [`govp.io`](https://github.com/govp-protocol/govp.io) | Documentation, normative publication and local browser verifier | MIT |

The protocol is not tied to Python. Its wire behavior is defined by the
normative text and conformance vectors. Independent Go, Rust, JavaScript and
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
