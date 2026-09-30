# VGO Diagnosis v1.0 — Error, Event & Compatibility Registry
**Status: FROZEN — 2026-10-01**

## Error registry
| Code | HTTP | Retry | Meaning |
|---|---:|---|---|
| INVALID_REQUEST | 400 | no | schema/semantic input invalid |
| INVALID_SCOPE | 400 | no | scope not usable for requested operation |
| BASELINE_REQUIRED | 400 | no | retest missing baseline |
| ENTITY_NOT_FOUND | 404 | no | entity inaccessible/not found |
| SCOPE_NOT_FOUND | 404 | no | scope inaccessible/not found |
| RUN_NOT_FOUND | 404 | no | run inaccessible/not found |
| EVIDENCE_NOT_FOUND | 404 | no | evidence inaccessible/not found |
| FORBIDDEN | 403 | no | authorization denied |
| TENANT_MISMATCH | 403 | no | resource belongs to another subject |
| PROTECTED_RESOURCE | 403 | no | sealed/protected resource unavailable |
| BASELINE_SCOPE_MISMATCH | 409 | no | baseline and retest scope incompatible |
| IDEMPOTENCY_KEY_REUSED | 409 | no | same key, different normalized body |
| RUN_NOT_CANCELLABLE | 409 | no | phase cannot be cancelled |
| RUN_NOT_TERMINAL | 409 | yes | requested result before terminal |
| RETEST_ONLY | 409 | no | operation valid only for retest |
| INSUFFICIENT_EVIDENCE | 422 | no | cannot start/complete meaningful requested evaluation |
| RATE_LIMITED | 429 | yes | quota/rate exceeded; Retry-After required |
| PROVIDER_UNAVAILABLE | 503 | yes | required external collection temporarily unavailable |
| PROTOCOL_UNAVAILABLE | 503 | yes | required protocol/manifest unavailable |
| INTERNAL_ERROR | 500 | yes | unexpected internal error |

Messages are explanatory, codes are program contracts. details MUST be redacted and MUST NOT expose sealed questions/provider secrets/stacks.

## Event registry
diagnosis.run.started; diagnosis.run.progressed; diagnosis.run.completed; diagnosis.run.insufficient_evidence; diagnosis.run.failed; diagnosis.run.cancelled; diagnosis.integrity.restricted; diagnosis.retest.completed; diagnosis.verification.completed.

Event envelope required fields: event_id, type, created_at, payload_version, aggregate_id, correlation_id, data. Delivery at-least-once. event_id globally unique. Consumer dedupe required. Breaking payload change increments payload_version; additive fields are compatible.

## Compatibility
HTTP v1: additive optional fields allowed; required-field additions/removal/reinterpretation require v2. Finding codes are stable/additive within diagnosis protocol v1. Metric formula/denominator/NA semantic changes require a new metric/protocol version. Protocol manifests remain retrievable for historical artifacts. Terminal artifacts are never silently recomputed under newer protocol.
