# VGO Framework v1.0 — Engineering Work Breakdown & Acceptance Matrix
**Status: EXECUTABLE DELIVERY BASELINE — 2026-10-01**

## Sequencing
Phase A contracts/schema → Phase B registries/storage → Phase C measurement/evidence → Phase D diagnosis/integrity → Phase E partner integration → Phase F conformance/operations → Rank F01–F08. Do not begin formal Rank signing before F08.

## Tasks
| ID | Deliverable | Depends | Acceptance evidence |
|---|---|---|---|
| VGO-001 | ProtocolRegistry tables + immutable manifests | — | publish/read version; digest stable; protected manifest inaccessible |
| VGO-002 | EntityRegistry + alias/disambiguation | 001 | same-name, brand/product, rename tests |
| VGO-003 | ScopeRegistry | 002 | market/locale/industry/question-space immutable scope |
| VGO-004 | Diagnosis DB migrations | 001-003 | forward/rollback; constraints/indexes |
| VGO-005 | EvidenceLedger storage | 004 | append-only; provenance family; conflict group; snapshot digest |
| VGO-006 | Measurement plan generator | 001,003 | pre-registration; outcome-blind retry plan |
| VGO-007 | SurfaceAdapter interface | 006 | shared failure mapping; protected material server-side |
| VGO-008 | Search adapter(s) | 007 | raw hashes/metadata/failure fixtures |
| VGO-009 | AI/answer adapter(s) | 007 | same |
| VGO-010 | Social adapter gate | 007 | disabled unless market protocol published |
| VGO-011 | Observation normalizer | 007-010 | no provider failure→absence |
| VGO-012 | Adjudication engine | 005,011 | P/U/C/R/NA/paid/error fixtures; append override |
| VGO-013 | Metric registry/calculator | 012 | denominator/coverage/version mandatory |
| VGO-014 | Finding engine | 012-013 | deterministic IDs; taxonomy |
| VGO-015 | Recommendation engine | 014 | action classes/guardrails/verification expectation |
| VGO-016 | Integrity engine | 005,012 | signal→review→verified/dismissed/recovered; no opaque penalty |
| VGO-017 | Diagnosis orchestrator/state machine | 004,006,012-016 | all legal/illegal transitions |
| VGO-018 | Retest comparator | 017 | resolved/persistent/regressed/new/incomparable |
| VGO-019 | Verification request flow | 018 | action ref→independent retest |
| VGO-020 | REST API | 017-019 | OpenAPI conformance; stable errors |
| VGO-021 | OAuth/resource authorization | 020 | tenant/delegation/scope negative tests |
| VGO-022 | Idempotency/rate limiting | 020 | duplicate and body-conflict tests; Retry-After |
| VGO-023 | Outbox/webhooks | 017 | duplicate/reorder/replay/dead-letter tests |
| VGO-024 | Audit/observability | all | correlation IDs; no protected-content leakage |
| VGO-025 | SDK generation TS | 020 | generated from pinned OpenAPI; sample integration |
| VGO-026 | SDK generation Python | 025 | parity tests |
| VGO-027 | Sandbox fixtures | 020 | no-site, conflicts, outage, retest |
| VGO-028 | Omseek contract test harness | 019-023 | finding→task/change→verification→retest; no score override |
| VGO-029 | Conformance suite D01-D20 | 001-028 | all green with run IDs |
| VGO-030 | Security/privacy review | 021-024 | isolation, redaction, secret/KMS review |
| VGO-031 | Migration/rollback rehearsal | 004-005 | representative dataset pass |
| VGO-032 | Diagnosis release gate | 029-031 | signed release checklist; status=production available |
| VGO-033 | Developer Center update | 032 | actual routes/scopes/errors/SDKs match deployed version |
| VGO-034 | Rank integration | 005,012,016,032 | eligible snapshot handoff only |
| VGO-035 | Rank F01-F08 | existing Rank spec | formal signing remains disabled until F08 |

## Definition of ready for each task
Normative doc/schema identified; inputs/outputs known; failure modes known; test fixture listed; no unresolved semantic decision.

## Definition of done
Code reviewed; migration where needed; unit/integration/contract/security tests green; structured audit/metrics; docs generated/updated; rollback known; no TODO affecting semantics.

## Required CI jobs
openapi-lint; schema-compat; unit; integration-postgres; state-machine; deterministic-fixtures; authz-isolation; protected-data-leak; webhook-replay; sdk-ts; sdk-python; migration-forward-back; conformance-d01-d20.

## Release blocking rules
Any D01-D20 failure blocks Diagnosis production label. Any protected-question leak is P0 and invalidates affected test/production material. Any cross-tenant evidence read is P0. Any ability for partner to set final adjudication/metric/VR is P0. Rank F08 failure blocks formal certificates/badges/rankings but does not block already-validated Diagnosis.
