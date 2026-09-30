# VGO Diagnosis Service v1.0
**Status: FROZEN DEVELOPMENT CONTRACT — 2026-10-01**

## 1. Purpose
Framework-owned evidence-backed diagnosis for a defined entity/scope: where and why machine-world effective visibility is weak, wrong, untrusted or unstable, and what should be verified next. It is not Rank, a certificate, guaranteed business outcome, or Omseek-private score.

## 2. Input
Request uses existing entity_id and scope_id; mode baseline|retest. Scope pins entity type, market, locale, industry/question space and surfaces. Website/domain is optional. Caller may submit authorized canonical facts and source references as candidate evidence, never final dimension scores/adjudication.

## 3. Dimensions
1 Entity identity/canonical facts; 2 machine-readable foundation/VHI (no website => not_applicable, never zero); 3 search discoverability; 4 AI/answer visibility; 5 understanding/factual accuracy; 6 evidence/citation trust; 7 comparison/recommendation fitness; 8 social/distributed discovery where protocol exists; 9 integrity/poisoning risk; 10 freshness/consistency.

Each dimension returns supported|unsupported|not_applicable|insufficient_evidence plus evidence-backed findings. Numeric indicators require a versioned denominator/uncertainty protocol; no invented precision.

## 4. Objects
DiagnosisRun pins ids, mode, state, versions, correlation_id, baseline_run_id, input_digest, evidence_snapshot_id and timestamps. Finding has stable id, dimension, severity info|low|medium|high|critical, status, code, claim, evidence_refs, contrary_evidence_refs, confidence, surfaces and protocol version. Recommendation has finding_id, objective, action_class, rationale, expected_verification, constraints. DiagnosticMetric has metric_id, value|null, unit, denominator, interval, coverage, status and version. EvidenceSnapshot is immutable.

## 5. State
queued→planning→collecting→adjudicating→analyzing→completed. Terminal alternatives insufficient_evidence|failed|cancelled. restricted is a policy condition, never a low score. Completed runs pin immutable snapshot/input digest; retries create a new run.

## 6. Retest
Retest references baseline_run_id and reports resolved, persistent, new/regressed and incomparable findings. It MUST NOT claim causality without separate causal evidence.

## 7. Rank separation
Diagnostic public sets and formal sealed Rank sets are isolated. Diagnosis cannot assign VR0–VR10. Rank may reuse eligible evidence only through Framework-controlled lineage/eligibility.

## 8. Access
OAuth scopes diagnostics:run, diagnostics:read, optional evidence:read. Protected prompts/raw copyrighted evidence are not public. Omseek uses the same wire contract as equivalently authorized partners.

## 9. Acceptance D01–D10
D01 no-site/VHI N/A; D02 same-name disambiguation; D03 provider failure ≠ absence; D04 deterministic finding IDs for same snapshot/protocol; D05 terminal finding lineage or explicit insufficient state; D06 retest/version-break diff; D07 no sealed-question leakage; D08 tenant auth/redaction; D09 idempotency/webhook replay; D10 OpenAPI/examples/SDK generation CI. Only then advertise production availability.
