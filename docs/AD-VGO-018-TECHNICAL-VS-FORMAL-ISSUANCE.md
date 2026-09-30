# Architecture decision: Technical issuance vs Formal Rank issuance

**ID:** AD-VGO-018  
**Status:** FROZEN — 2026-10-01  
**Supersedes:** Informal 2026-09-30 emergency wording that treated F08 as optional for all issuance claims

## Doctrine (normative)

**Technical Issuance Enabled ≠ Formal Rank Issuance Authorized.**

These are two independent gates. Documents, portals, and operators MUST NOT collapse them.

## Gate 1 — Technical issuance (Status 3)

**Enables:** `ISSUANCE_ENABLED=1` on production after SoftHSM (or equivalent HSM) JWKS is non-empty and dual human approval (STD request ≠ GOV approval) is recorded.

When Gate 1 passes:

- The full production signing chain MAY run (score pipeline, JWS issue, status transitions, revoke).
- Issued production certificates MUST remain in **`provisional`** state per [VGO-RANK-STANDARD-V1.0.md](VGO-RANK-STANDARD-V1.0.md) §5 / §7 until Formal Authorization.
- **Trial strip / trial badge** MAY be shown for provisional certificates; MUST NOT be presented as the official dynamic badge or formal certification mark.
- **Verify, revoke, and webhook** paths MAY operate on production with real signatures and fail-closed semantics.
- Public **formal badge**, **approved public rankings**, and **U4-style “formal issuance is open”** announcements MUST NOT be claimed.

## Gate 2 — Formal Rank issuance (F08 + governance)

**Hard-gates:** formal qualification, official badge, public rankings, and U4 external messaging.

F08 (calibration quality package: queue, pre-registration, dual 30-day windows, public calibration report, quality gates) blocks **Formal Authorization**, NOT the technical production signing path.

F08 is **not cancelled**. It remains mandatory before any entity or certificate is promoted from provisional trial semantics to formal rated semantics at scale.

When Gate 2 passes and governance records **`provisional → rated`** for an eligible entity/certificate:

- **Formal Certificate** (rated state) MAY be issued or affirmed.
- **Official Badge** and **Public Ranking** surfaces MAY open per release and legal gates.
- **U4** external announcement MAY proceed when website/platform checklist evidence is also complete.

## State vocabulary (do not merge)

| Term | Meaning |
|------|---------|
| Implemented / Validated / Production available | Engineering baseline §7 — not formal Rank |
| Technical Issuance Enabled | Gate 1 — provisional production certs allowed |
| Formal Rank Issuance Authorized | Gate 2 — F08 complete + governance promotion to rated |
| Formally rated | F08 passed; rated certificates and approved public listings |

## Consequences

- Website Status 3 copy: signing path enabled; formal issuance not announced; provisional = trial per standard.
- Developer center L1: formal badge and rankings require Formal Authorized; trial presentation is a separate, labeled surface; dual OpenAPI (`rank-openapi-v1.0.yaml`, `diagnosis-openapi-v1.0.yaml`) unchanged.
- Operators MUST disclose incomplete F08 until Gate 2 passes; MUST NOT claim “first calibration accepted” or “formal rating in operation” under Status 3 alone.

## References

- [VGO-ENGINEERING-BASELINE-V1.0.md](VGO-ENGINEERING-BASELINE-V1.0.md) §5 Release gates  
- [VGO-RANK-STANDARD-V1.0.md](VGO-RANK-STANDARD-V1.0.md) §5 / §7 (`provisional` = trial; no formal badge or leaderboard)  
- [DEVELOPER-CENTER-COMPLETE-V1.0.md](DEVELOPER-CENTER-COMPLETE-V1.0.md)  
- [RANK-SERVICE-ARCHITECTURE-V1.0.md](RANK-SERVICE-ARCHITECTURE-V1.0.md) F08
