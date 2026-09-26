# Candidate decision record: VGO Rank and Framework diagnostic/rating capabilities

**ID:** AD-VGO-017 (candidate)  
**Status:** Proposed; pending framework governance review  
**Date:** 2026-09-26

## Decision proposed

Make VGO Framework the owner of the public VGO Rank standard and the shared diagnostic/rating capability boundary. Framework defines protocols, metrics, calibration, certificate lifecycle, and appeal rules, and is the sole formal issuer of VGO Rank. Omseek consumes Framework interfaces for customer diagnosis, action planning, optimization, and retesting.

## Rationale

This extends VGO from a method for guiding action into an end-to-end operational framework: define target intent and evidence → observe → diagnose → rate → identify gaps → guide action → execute → retest → evaluate outcomes. Rank is the public rating output within that chain, not the whole Framework. Consistent ownership enables future implementations to use the same protocol and certificate semantics.

## Required safeguards

- Formal rating eligibility, sampling, and issuance are the same for Omseek customers and non-customers.
- Payment may expand private diagnostic depth or frequency but cannot change formal Rank inputs, thresholds, appeals, or outcomes.
- Certificates disclose the standards owner, evidence provider, issuer, appeal reviewer, and relevant Omseek relationship.
- Do not claim independent governance, independent validation, industry authority, or broad adoption before those conditions are evidenced.
- Keep exact weights, thresholds, minimum samples, and production API versions open until empirical calibration and review.

## Adoption tests and follow-up

Before implementation binding, map this proposal to the applicable contract decisions and tests, including AD-VGO-017 decision-driven behavior, AD-VGO-015 evidence drill-down, and AD-PROD-013 semantic-boundary checks where those contracts apply. Update status-machine/API documents only in the implementation phase, then run the repository's `npm run check:contracts` gate in the implementation repository. This documentation proposal alone does not claim those implementation gates passed.

## Consequences

VGO Framework requires separately versioned Rank, measurement, governance, and API documents. Omseek becomes a Framework API consumer and commercial implementation. A first single-market pilot, calibration report, appeal process, conflict disclosure, and legal review are prerequisites to formal public issuance.
