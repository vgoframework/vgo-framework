# VGO Framework ↔ Omseek Contract v1.0
**Status: FROZEN BOUNDARY — 2026-10-01**

Framework is authority for VGO semantics, measurement, shared evidence semantics, Diagnosis, VHI semantics, Rank/certificates. Omseek is a VGO implementation and commercial **effective-visibility growth and optimization platform** owning customer workflow, private truth/assets, opportunity planning, optimization execution, publishing integrations, monitoring/verification UX, governance workflow and commercial data.

Omseek→Framework: entity/scope candidates, authorized canonical facts, asset/source references, diagnosis/retest/rating requests, appeals/corrections. Framework→Omseek: IDs, measurement status, authorized evidence summaries, diagnostic metrics/findings/recommendations, integrity states, retest diffs, rating status and signed certificate/status.

Omseek converts findings into Missions/Tasks/ChangeSets, seeks approvals, executes, records execution evidence, then requests verification/retest. Framework decides diagnostic observation semantics and formal Rank eligibility/results.

Omseek MUST NOT recalculate/override VR, relabel its own score as VGO Rank, write Framework formal evidence, access sealed questions, convert provider failure to absence, suppress contrary evidence, or treat paid optimization as rating privilege.

Cross-system IDs: correlation_id, entity_id, scope_id, diagnosis_run_id, finding_id, evidence_id, baseline_run_id, rating_request_id, certificate_id. Integrators store these rather than infer identity from names.

Delivery is at-least-once. Consumers dedupe event_id, tolerate reorder, and query authoritative state. Certificate revocation/expiry fails closed. Protocol-version breaks create explicit incomparability, never silent normalization.
