# VGO v1.0 Conformance & Acceptance
**Status: FROZEN TEST BASELINE — 2026-10-01**

A conforming implementation passes contract/schema, deterministic calculation, state-machine, provenance, isolation, integrity and interoperability suites.

Golden cases MUST include: no website; same-name entity; brand vs product; provider outage; stale first-party fact; conflicting independent evidence; syndicated sources masquerading as multiple sources; paid placement; AI answer with no explicit citation; recommendation N/A; wrong entity; protected question leakage attempt; retest after action; protocol version break; insufficient evidence; duplicate/reordered webhook; idempotency-key body conflict; cross-tenant evidence request; restricted/revoked certificate.

Negative assertions: provider failure never becomes entity absence; no-site never becomes VHI=0; unrated never becomes VR0; Diagnosis never emits VR; partner cannot set adjudication/final score; no terminal finding without lineage/insufficient state; no protected prompt in API/log/webhook; no revoked/expired certificate cached as active beyond contract.

Release evidence must contain schema hashes, protocol manifests, test run IDs, migration/rollback result, security isolation result, known limitations and deployment status. Rank production signing remains separately gated by F08.
