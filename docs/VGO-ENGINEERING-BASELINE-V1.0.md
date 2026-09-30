# VGO Framework v1.0 Engineering Baseline
**Status: FROZEN ENGINEERING CONTRACT — 2026-10-01**

This is the engineering source-of-truth map for VGO shared measurement, diagnosis, Rank and governance. It does not claim production services passed release gates.

## 1. Normative architecture
**Specification → Measurement → Diagnosis → Governance/Action Contract → Re-measurement → Rank/Certificate**

VGO Framework owns shared semantic/computational contracts. Omseek and other products may implement workflow, customer assets, optimization and execution, but MUST NOT redefine VGO measurement semantics, mutate Framework evidence, calculate a competing VGO Rank, or bypass certificate state.

Precedence: Rank standard; Diagnosis service/OpenAPI; Measurement protocol; Evidence Ledger; Integrity contract; Framework↔Omseek contract; then existing Rank HTTP/certificate contracts. Older conflicting drafts are superseded.

## 2. Frozen boundaries
Framework owns entity/scope semantics, protocols, measurement, evidence lineage, adjudication semantics, Diagnosis, VHI semantics, Rank calculation/signing, certificates, appeals, integrity classifications and conformance tests. Integrators own customer workflow/private data/action planning/execution/UI. Diagnosis is not Rank. Rank never accepts caller-supplied final scores. unrated is never VR0. Website absence does not prevent entity diagnosis/rating; VHI is separate/N/A. Business outcomes validate usefulness but do not enter Rank directly.

## 3. Public vs protected
Public: definitions, dimensions, state semantics, evidence requirements, grade meanings, API schemas, certificate verification, change policy, conformance rules. Protected: sealed rating questions, anti-gaming signals, security heuristics, credentials/keys and unreleased calibration data. Protected parameters are versioned and audit-hashed; secrecy cannot change public result semantics.

## 4. Independent version axes
Persist api_version, diagnosis_protocol_version, measurement_protocol_version, question_space_version, surface_protocol_version, adjudication_version, integrity_policy_version, rank_protocol_version, schema_version and build_id. Every terminal artifact pins applicable versions plus immutable input digest.

## 5. Release gates
Production requires OpenAPI/schema lint, deterministic fixtures, state/idempotency/retry tests, tenant/role isolation, zero orphan terminal findings, sealed-question leakage tests, fail-closed integrity paths, webhook replay tests, migration/rollback and safe observability. Formal Rank additionally requires existing F08. Diagnosis may ship independently after D01–D10.

## 6. Work packages
EB01 ProtocolRegistry/version manifests; EB02 Entity/scope registry; EB03 measurement scheduler/adapters; EB04 EvidenceLedger; EB05 adjudication; EB06 Diagnosis; EB07 integrity engine; EB08 governance bridge; EB09 existing Rank F01–F08; EB10 public registry/developer center; EB11 conformance suite; EB12 legacy deprecation/contract diff.

## 7. Definition of done
Implemented = code+migration+API+tests+observability+security. Validated = applicable acceptance suite passes. Production available = deployment/operational gates also pass. Formally rated = Rank F08 also passes. Documents MUST NOT collapse these states.
