# VGO Evidence Ledger & Lineage v1.0
**Status: FROZEN ENGINEERING CONTRACT — 2026-10-01**

No material Diagnosis finding, metric or Rank artifact may exist without reconstructable provenance. Formal evidence is append-only; corrections append superseding events.

Minimum record: evidence_id, entity_id, scope_id, observation_id, evidence_type, source_class, source_locator/redacted_locator, collected_at, valid_at, market, locale, surface, provider, raw_content_hash, normalized_content_hash, parser_version, authorization_class, retention_class, lineage_parent_ids, conflict_group_id, created_at.

Source classes include first-party official, authoritative registry, independent editorial/media, platform-native, user-generated, partner-supplied and unknown. Mirrors/syndication from one origin are one provenance family, not independent corroboration.

Terminal computation pins EvidenceSnapshot: ordered evidence IDs, cutoff, eligibility policy/version and digest. Same snapshot/protocol/build is deterministic except explicitly versioned stochastic procedures with fixed seed.

Contradictory claims form conflict groups. Resolution records basis/reviewer; unresolved material conflict remains visible and may trigger restriction. Staleness is protocol-relative and never silently overwritten.

Public certificate summaries expose necessary aggregates/hashes only. Raw customer evidence requires authorization. Lawful byte deletion uses permitted minimal metadata/hash/tombstone without falsifying historical audit events.

Invariants: no orphan finding; no mutable signed snapshot; no cross-tenant raw-evidence read; no certificate without input snapshot; no false independent corroboration.
