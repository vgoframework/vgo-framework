# VGO Diagnosis v1.0 — Full Engineering Implementation Specification
**Status: FROZEN IMPLEMENTATION CONTRACT — 2026-10-01**  
**Normative owner: VGO Framework**  
**Applies to:** Framework service, Omseek integration, authorized partners, SDKs, conformance tests.

## 0. Normative language and precedence
MUST/MUST NOT/SHOULD/MAY are normative. Rank semantics remain governed by VGO-RANK-STANDARD-V1.0.md. This specification governs Diagnosis runtime behavior. diagnosis-openapi-v1.0.yaml governs HTTP wire shape. Where examples conflict with schemas, schemas win. Protected operational parameters never change public result semantics.

## 1. Service boundary
Framework owns: entity/scope identity; protocol registry; question-set classes; measurement scheduling; observation normalization; evidence ledger; adjudication; diagnostic metrics/findings/recommendations; integrity classification; retest comparison; Rank handoff eligibility; audit and public protocol manifests.
Clients own: customer authorization; canonical-fact candidates; assets; actions; approvals; execution; commercial workflow. Clients cannot set observation labels, metric values, findings, evidence eligibility, integrity disposition, Rank inputs/final scores, or sealed questions.

## 2. Runtime components
1. EntityRegistry
2. ScopeRegistry
3. ProtocolRegistry
4. DiagnosisOrchestrator
5. MeasurementPlanner
6. SurfaceAdapters
7. ObservationNormalizer
8. EvidenceLedger
9. Adjudicator
10. DiagnosticAnalyzer
11. IntegrityEngine
12. RetestComparator
13. EventOutbox
14. AuditLog
15. AuthorizationPolicy
16. PartnerAPI

Every component emits correlation_id and structured audit events. Formal evidence writes are append-only.

## 3. Persistence model
### 3.1 diagnosis_run
Fields: id UUID/ULID; tenant_subject; entity_id; scope_id; mode baseline|retest; baseline_run_id nullable; state; policy_condition nullable; requested_by; requested_at; started_at; completed_at; measurement_protocol_version; diagnosis_protocol_version; question_space_version; surface_protocol_versions JSON; adjudication_version; integrity_policy_version; schema_version; build_id; input_digest; evidence_snapshot_id nullable; failure_code nullable; failure_detail_redacted nullable; created_at.
Indexes: entity_id+scope_id+requested_at; state+requested_at; baseline_run_id.
Invariant: completed/insufficient_evidence terminal rows are immutable except append-only annotations.

### 3.2 diagnosis_dimension_result
run_id; dimension_id; status supported|unsupported|not_applicable|insufficient_evidence; summary; evidence_coverage numerator/denominator; confidence nullable; metric_refs[]; finding_refs[]; protocol_version. PK run_id+dimension_id.

### 3.3 diagnostic_metric
id; run_id; metric_id; status; value nullable; unit; numerator nullable; denominator nullable; interval_low/high nullable; evidence_coverage; protocol_version; snapshot_digest. Numeric value MUST be null when status is unsupported/not_applicable/insufficient_evidence.

### 3.4 finding
id deterministic from run snapshot+protocol+canonical finding key; run_id; dimension; severity; status open|resolved|persistent|regressed|informational; code; title; claim; rationale; evidence_refs[]; contrary_evidence_refs[]; confidence; affected_surfaces[]; first_seen_at; last_seen_at; protocol_version. Material positive/negative claims require evidence; insufficient-evidence findings explicitly use evidence_gap codes.

### 3.5 recommendation
id; run_id; finding_id; objective; action_class; rationale; expected_verification; constraints[]; priority_class P0|P1|P2|P3; human_approval_required boolean; prohibited_actions[]; protocol_version. Recommendation is guidance, not autonomous authority over third-party systems.

### 3.6 observation
id; plan_item_id; run_id; surface; provider; entry; question_id; question_class; scheduled_batch; collected_at; collection_status success|timeout|blocked|transport_error|parser_error|policy_unavailable; raw_request_hash; raw_response_hash nullable; evidence_refs[]; provider_metadata_redacted; parser_version. Failure is never entity absence.

### 3.7 adjudication
id; observation_id; P/U/C/R nullable booleans; na_reasons; paid_placement; identity_error; material_fact_error; integrity_flags[]; adjudicator_type automated|human; reviewer_id nullable; adjudication_version; supersedes_id nullable; created_at. Overrides append rows.

### 3.8 evidence / evidence_snapshot
Follow EVIDENCE-LEDGER-V1.0.md. Snapshot contains ordered evidence IDs, eligibility policy/version, cutoff, digest. Terminal run MUST reference snapshot unless failed/cancelled before evidence collection.

### 3.9 integrity_case
id; entity_id; scope_id; run_id nullable; category; disposition; severity; confidence; evidence_refs[]; contrary_evidence_refs[]; reviewer; policy_version; opened_at; resolved_at; recovery_evidence_refs[].

### 3.10 outbox_event
event_id; aggregate_type; aggregate_id; event_type; payload_version; payload; created_at; published_at nullable; attempts; last_error_redacted. Unique event_id. At-least-once delivery.

## 4. Diagnosis dimensions and minimum metrics
D1 identity: identity_conflict_count, canonical_fact_coverage.
D2 VHI: foundation_check_coverage plus protocol-defined site metrics; no owned web asset => dimension not_applicable and all VHI metrics null.
D3 search: eligible_opportunities, presence_rate, effective_presence_rate.
D4 AI/answer: eligible_opportunities, answer_presence_rate, answer_effective_rate, citation_readiness where applicable.
D5 understanding: factual_accuracy_rate, entity_disambiguation_accuracy.
D6 evidence trust: traceable_evidence_rate, independent_corroboration_rate, stale_evidence_rate.
D7 comparison/recommendation: eligible_recommendation_opportunities, reasonable_recommendation_rate; information-only opportunities are NA.
D8 social/distributed: only when published market surface protocol exists.
D9 integrity: verified_risk_count, unresolved_material_conflict_count; no opaque punitive score.
D10 freshness/consistency: cross_surface_conflict_rate, stale_fact_rate, temporal_drift indicators.

Metric formulas MUST be registered in ProtocolRegistry. The service MUST NOT emit a metric whose denominator/NA rules/version are absent. Diagnosis may expose rates 0..1 or percentages, but MUST include denominator and coverage. Confidence intervals are optional only if the metric protocol says so.

## 5. Finding taxonomy
Codes are stable machine contracts. Initial namespaces:
IDENTITY_*: AMBIGUOUS_ENTITY, OFFICIAL_FACT_CONFLICT, PRODUCT_BRAND_CONFUSION.
FOUNDATION_*: OWNED_ASSET_MISSING, CRAWL_BLOCKED, CANONICAL_INCONSISTENT, STRUCTURED_FACT_GAP, CONTENT_STALE.
SEARCH_*: NONBRAND_ABSENCE, LOW_EFFECTIVE_PRESENCE, RESULT_FACT_ERROR.
ANSWER_*: ANSWER_ABSENCE, ANSWER_FACT_ERROR, CITATION_GAP, SOURCE_MISMATCH.
TRUST_*: SINGLE_PROVENANCE_DEPENDENCE, STALE_CORROBORATION, UNTRACEABLE_CLAIM.
RECOMMEND_*: RELEVANCE_MISMATCH, UNSUPPORTED_RECOMMENDATION, COMPARISON_FACT_ERROR.
INTEGRITY_*: ENTITY_CONFUSION, FABRICATED_EVIDENCE, PROVENANCE_CONCENTRATION, COORDINATED_MANIPULATION, COMPROMISED_FIRST_PARTY, PROMPT_INJECTION_CONTENT.
FRESHNESS_*: CROSS_SURFACE_CONFLICT, TEMPORAL_DRIFT.
EVIDENCE_*: INSUFFICIENT_COVERAGE, PROVIDER_UNAVAILABLE, REVIEW_REQUIRED.
New codes are additive in v1. Existing code semantics cannot be redefined without a protocol major version.

## 6. Recommendation action classes
CANONICAL_FACT_FIX; OWNED_ASSET_FIX; STRUCTURED_DATA_FIX; CONTENT_EVIDENCE_IMPROVEMENT; SOURCE_CORRECTION_REQUEST; EXTERNAL_CORROBORATION; ENTITY_DISAMBIGUATION; FRESHNESS_UPDATE; INTEGRITY_RESPONSE; MEASUREMENT_RETRY; HUMAN_REVIEW; NO_ACTION_OBSERVE.
Prohibited: fake reviews, fabricated sources, impersonation, hacking, deceptive paid placement, competitor poisoning, safeguard bypass.

## 7. State machine
Allowed:
queued→planning|cancelled
planning→collecting|insufficient_evidence|failed|cancelled
collecting→adjudicating|insufficient_evidence|failed|cancelled
adjudicating→analyzing|insufficient_evidence|failed
analyzing→completed|insufficient_evidence|failed
Terminal: completed, insufficient_evidence, failed, cancelled.
No transition out of terminal. Retest is a new run. restricted is policy_condition, not run state.
Cancel is best-effort; after adjudicating starts, cancellation MAY be rejected with RUN_NOT_CANCELLABLE.

## 8. API operations
Required v1 operations:
POST /v1/diagnosis-runs
GET /v1/diagnosis-runs/{id}
POST /v1/diagnosis-runs/{id}/cancel
GET /v1/diagnosis-runs/{id}/dimensions
GET /v1/diagnosis-runs/{id}/metrics
GET /v1/diagnosis-runs/{id}/findings
GET /v1/diagnosis-runs/{id}/recommendations
GET /v1/diagnosis-runs/{id}/evidence-summary
GET /v1/diagnosis-runs/{id}/retest-diff (retest only)
POST /v1/diagnosis-runs/{id}/verification-requests
GET /v1/protocols/diagnosis/{version}
GET /v1/protocols/measurement/{version}
POST /v1/webhook-subscriptions and delete/rotate operations may reuse Rank platform subscription contract if payload namespaces are shared.

Raw evidence endpoint is optional/privileged and requires evidence:read; evidence summary is mandatory.

## 9. Idempotency, concurrency and retry
POST create/cancel/verification use Idempotency-Key. Key retention minimum 24h. Same key+same normalized body returns original semantic response; same key+different body => 409 IDEMPOTENCY_KEY_REUSED.
Create run uniqueness does NOT dedupe different keys automatically; clients explicitly reference baseline/retest.
Optimistic concurrency for mutable partner resources uses ETag/If-Match where applicable.
429 includes Retry-After. Retryable 5xx and transport failures use exponential backoff+jitter. Client retries MUST NOT create duplicate runs when same key is reused.

## 10. Error contract
Envelope: code, message, retryable, request_id, details.
Stable codes:
INVALID_REQUEST 400; INVALID_SCOPE 400; BASELINE_REQUIRED 400; BASELINE_SCOPE_MISMATCH 409; IDEMPOTENCY_KEY_REUSED 409; RUN_NOT_CANCELLABLE 409; RUN_NOT_TERMINAL 409; RETEST_ONLY 409; ENTITY_NOT_FOUND 404; SCOPE_NOT_FOUND 404; RUN_NOT_FOUND 404; EVIDENCE_NOT_FOUND 404; FORBIDDEN 403; PROTECTED_RESOURCE 403; TENANT_MISMATCH 403; RATE_LIMITED 429; PROVIDER_UNAVAILABLE 503; PROTOCOL_UNAVAILABLE 503; INSUFFICIENT_EVIDENCE 422 when synchronous validation cannot start; INTERNAL_ERROR 500.
Do not leak provider secrets, sealed questions, raw protected evidence or internal stack traces.

## 11. Authorization matrix
diagnostics:run create/retest/verification; diagnostics:read run/dimensions/metrics/findings/recommendations/diff/summary; evidence:read authorized raw evidence only; protocols:read manifests; subscriptions:write webhook management.
Resource authorization also checks tenant_subject, customer delegation, scope authorization and environment. OAuth scope alone is insufficient.
Omseek and partners receive no issuer/signing privileges through Diagnosis scopes.

## 12. Webhook events
diagnosis.run.started; diagnosis.run.progressed; diagnosis.run.completed; diagnosis.run.insufficient_evidence; diagnosis.run.failed; diagnosis.run.cancelled; diagnosis.integrity.restricted; diagnosis.retest.completed; diagnosis.verification.completed.
Envelope: event_id, type, created_at, payload_version, aggregate_id, correlation_id, data. At-least-once; consumers dedupe. Delivery signing uses the platform webhook scheme, timestamp window and replay protection. Webhook never contains sealed questions/raw protected evidence.

## 13. Measurement adapter contract
Adapter input: plan_item_id, surface_protocol_version, query/prompt material reference (server-side for protected sets), locale/region/device/interface/session constraints, timeout budget.
Adapter output: collection_status, provider/product identifiers, visible model/index identifier if available, raw request/response secure references+hashes, timestamps, provider metadata allowlist.
Adapters MUST NOT adjudicate business meaning. They MAY identify technical parser fields. Provider-specific failures map to shared collection_status.

## 14. Evidence eligibility
Evidence eligibility is determined by policy version, authorization, provenance, time, scope and integrity state. Partner-supplied evidence is candidate evidence until Framework validation. Syndicated copies share provenance family. Paid content is labeled. Conflicting evidence is never discarded solely because it is unfavorable.

## 15. Retest comparability
Comparable only when scope identity and required protocol dimensions remain compatible. Diff states: resolved, persistent, regressed, new, incomparable. A version break records reason and affected metrics/findings. No causal claim from temporal association alone.

## 16. Verification request
Omseek may submit action metadata/change-set references and request verification. Framework receives only necessary execution evidence/candidate facts; it independently schedules measurement. Caller cannot specify desired finding outcome. Verification creates or links a retest run.

## 17. Security/privacy
Secrets in managed secret store/KMS; no secrets in logs. Raw evidence encrypted at rest/in transit. Tenant isolation enforced in query layer and service authorization. Audit actor for human override. PII minimized. Protected prompt material server-side only. Logs redact prompts where protected. Abuse controls rate-limit enumeration of entities/evidence.

## 18. Observability/SLO semantics
Metrics: queue latency, run duration by phase, adapter success/failure by class, evidence coverage, adjudication backlog, webhook lag, error code rate. Traces carry request_id/correlation_id/run_id but not protected raw content. SLO targets are deployment policy, not protocol semantics.

## 19. Migrations/versioning
HTTP /v1 additive optional fields allowed. Removing/reinterpreting fields requires /v2. Protocol versions are independent of HTTP version. Database migrations are forward+rollback tested. Historical terminal artifacts remain readable under their pinned schema/protocol. New protocol cannot silently recompute old result.

## 20. Conformance acceptance
D01 no-site => VHI N/A/null metrics.
D02 same-name disambiguation prevents evidence mixing.
D03 provider failure never P=0.
D04 same snapshot/protocol/build yields deterministic finding IDs/results.
D05 no terminal material finding without lineage or explicit evidence gap.
D06 retest diff handles protocol breaks.
D07 no sealed question in API/log/webhook/client trace.
D08 cross-tenant raw evidence denied.
D09 idempotency duplicate/reused-body conflict.
D10 OpenAPI lint+SDK generation.
D11 invalid state transitions rejected.
D12 partner cannot submit metric/final adjudication/VR.
D13 syndicated evidence not counted independent.
D14 paid placement labeled and excluded where protocol requires.
D15 integrity verified risk restricts without undocumented score penalty.
D16 webhook duplicate/reorder/replay safe.
D17 cancellation semantics correct.
D18 terminal snapshot immutable.
D19 migrations rollback on representative dataset.
D20 Framework↔Omseek contract test: finding→action→verification→retest with no Omseek scoring authority.

All D01–D20 MUST pass for Diagnosis v1 production readiness.
