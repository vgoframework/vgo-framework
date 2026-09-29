# Governance

The VGO is an open methodology initiated and maintained by Omseek.

## Roles
- **Maintainers:** decide releases, merge proposals and protect conceptual coherence.
- **Contributors:** propose definitions, metrics, research, examples and corrections.
- **Reviewers/Domain experts:** may provide non-binding technical or industry review.

## Decision model
Community contribution does not imply automatic acceptance. Maintainers may accept, revise, defer or reject proposals. Material changes should include rationale in the repository history.

## Neutrality of the system
The system should distinguish general VGO methodology from Omseek-specific product features. Omseek implementations may extend the system, but proprietary behavior should not be presented as a universal VGO requirement.

## Public evaluation
Published evaluation cases should follow [EVALUATION-PROTOCOL.md](EVALUATION-PROTOCOL.md): disclose the protocol version, sample denominator, four conclusion counts, missing cases, and conflicts of interest. Dual independent coding is required. Omseek private scores do not resolve disagreements. External comments do not imply endorsement of VGO.

## Action and automation proposals

Proposals for new action methods should identify inputs, a responsible actor, a concrete output, verification evidence, failure modes and any required human review. Automation proposals must state which steps can be automated and which require approval or override. Proprietary Omseek behavior must not be claimed as a universal VGO requirement.

## Versioning
- Patch: wording/clarification without conceptual change.
- Minor: backward-compatible additions.
- Major: material changes to scope, pillars or definitions.

## VGO Rank and shared capabilities

VGO owns the public definitions, measurement and evidence protocol, metric semantics, rating levels, calibration policy, versioning, and appeal rules for VGO Rank. The system is the intended authority for the shared diagnostic and rating interfaces and for issuing, suspending, or revoking formal certificates. VGO Rank v1.0 is a frozen normative protocol; formal issuance remains gated by its two pilot windows, calibration report, quality thresholds, conflict disclosures, legal review and revocation exercise. Until these pass, observed levels must be labeled as trials and must not claim formal certification, industry authority or independent third-party status. See [the Rank standard](docs/VGO-RANK-STANDARD-V1.0.md).

Omseek is the system's initiator, founding maintainer, and first product implementation. It may call system interfaces to deliver customer diagnosis, action guidance, optimization, and retesting. It must not override a formal Rank, change rating inputs for its customers, or adjudicate its own customers' appeals. Paid optimization may provide deeper or more frequent private diagnostics, but payment must not change formal rating eligibility, sampling protocol, or certificate outcome. Public cases and certificates must disclose the system/Omseek relationship and distinguish the standard owner, evidence provider, issuer, and appeal reviewer; shared roles must be disclosed. Apply the same formal protocol to Omseek, its customers, and non-customers.
