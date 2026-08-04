# GOVP

GOVP is an open protocol for portable evidence that can be verified without a
central service or a proprietary verifier.

It binds a published statement to exact artifact bytes, an issuer-controlled
technical identity and an Ed25519 signature. GOVP verifies integrity,
attribution and declared artifact binding. It does not make a claim true or
provide independent time unless an external timestamp or witness is present.

## Start here

- [Protocol source and reference verifier](https://github.com/govp-protocol/govp)
- [Official documentation](https://govp.io/govp/docs.html)
- [GOVP-1 normative specification](https://govp.io/govp/spec/govp-1.html)
- [Conformance vectors](https://govp.io/govp/conformance/vectors.json)
- [Browser verifier](https://govp.io/govp/verify.html)
- [Security policy](https://github.com/govp-protocol/govp/security/policy)

## Public repositories

| Repository | Responsibility | License |
|---|---|---|
| [`govp`](https://github.com/govp-protocol/govp) | Normative specification, schemas, conformance vectors and reference Python verifier | Apache-2.0 |
| [`govp.io`](https://github.com/govp-protocol/govp.io) | Official website, rendered documentation and browser verifier | MIT |

The `govp` repository is the canonical source for the protocol. The website
publishes checksum-verified copies of its normative artifacts.

## Stewardship

GOVP is stewarded by Gemacode, a brand of Brilyetz Holding S.L. Technical
conformance does not imply endorsement, certification or affiliation.

Security reports must be sent privately to
[`research@gemacode.org`](mailto:research@gemacode.org).
