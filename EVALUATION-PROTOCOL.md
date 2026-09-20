# VGO Public Evaluation Protocol — Draft 0.1

**Status:** Proposed addition to the VGO Framework; unvalidated and not part of the v1.0.0-draft release.  
**Purpose:** Enable independent reviewers to assess one documented user-intent scenario using the same evidence and explicit rules, without Omseek software. This protocol is not a certification or a universal scoring formula.

This document operationalizes the measurement principles in [METRICS.md](METRICS.md) and the integrity requirements in [INTEGRITY-AND-DEFENSE.md](INTEGRITY-AND-DEFENSE.md). It retains the existing VGO concepts of Effective Assets, Effective SEO, Effective GEO, and Effective Visibility. It introduces no new composite index. The conceptual expression “Right Audience × Right Intent × Right Surface × Right Presence” is not arithmetic.

## 1. Scope and unit of evaluation

The unit is **one predefined user-intent scenario, one entity, and one discovery surface under recorded conditions**. Version 0.1 is designed for search and generative AI; transfer to other surfaces remains a research question. A scenario-level finding does not establish an organization's overall market performance, customer preference, or sales impact. A ranking, mention, or citation is an observation, not an outcome.

A reviewer must record before collection:

| Field | Required record |
| --- | --- |
| Audience and need | User type, triggering need, concrete question, and decision stage |
| Intent basis | Source and date of interviews, support/sales records, site-search data, public questions, or other evidence; if absent, label the intent *unverified* |
| Entity and claims | Organization/product/service, facts material to this scenario, owned source URLs, and their update dates |
| Surface and query | Search engine or AI service, region, language, device/interface, exact query or full prompt, collection time, and visible model/version where available |
| Comparison set | Competitors or alternatives included, with inclusion reasons; do not select only favorable alternatives |
| Raw observations | Full result/answer snapshots, visible position and ad labels where relevant, cited URLs, and timestamps |
| Downstream evidence | Clicks, relevant visits, qualified leads or other outcomes when actually available, including the measurement definition |
| Review | Reviewer identities or stable pseudonyms, protocol version, judgments, evidence, counterevidence, and disagreements |

A “high-value” label requires a stated relation to real users, the decision stage, and the entity's actual offering, with the supporting source and limitations. Reviewers may mark it *supported*, *plausible but unverified*, or *unknown*; the protocol does not prescribe a proprietary discovery algorithm. Do not infer coverage of a high-value problem space from one occurrence.

## 2. Item-level judgments

For each dimension use **meets / does not meet / insufficient evidence / not applicable**, and cite evidence and counterevidence. No favorable item cancels a materially false claim.

| Dimension | Minimum basis for “meets” | Common failure or uncertainty |
| --- | --- | --- |
| Audience and intent relevance | Recorded query reasonably represents the stated user need; the entity's offering fits it | Invented low-value prompts, unstated need, irrelevant offering |
| Verifiable owned asset | Controlled, accessible asset supplies material, checkable facts and a maintenance signal where relevant | Missing/inaccessible asset, absent or stale key facts; existence alone is insufficient |
| Discovery | Entity or relevant asset appears under the recorded conditions in raw evidence | Branded-query result substituted for a non-branded scenario; old screenshot presented as current |
| Correct understanding | Material entity, product, scope, limitation and price facts in the observed result are not substantially distorted | Name collision, unsupported capability, stale price; mark insufficient if facts cannot be checked |
| Mention and citation | Separately record name appearance, quotation/citation, clickable source, and source quality | Mere mention reported as citation; untraceable or incorrect citation |
| Comparison and recommendation | If present, comparison or recommendation fits the need and verified facts | Sponsored placement or unsupported endorsement reported as user choice; if absent, mark not applicable |
| Integrity risk | Check entity confusion, stale/false claims, suspected manipulation and conflicting sources; preserve conflicts | Material unresolved conflict reported as trustworthy visibility |
| Outcome link | Report downstream behavior only with traceable evidence and a consistent measurement definition | Exposure or mentions represented as leads, purchases or incremental impact |

## 3. Scenario conclusion

Use one of four conclusions, scoped to this observation and surface:

- **Evidence-supported effective visibility:** Relevant audience and intent, documented appearance, correct material facts, and no unresolved material integrity risk. Explicitly state when downstream results are unknown. This is an evidence-based scenario judgment, not proof of actual selection.
- **Visible, but effectiveness not established:** Appearance is documented, but the scenario is irrelevant, facts are materially wrong, integrity risk remains unresolved, or the recommendation is unjustified.
- **No visibility observed:** The entity was absent under the preregistered sampling conditions. This does not prove absence for all users, prompts or times.
- **Insufficient evidence:** Query conditions, snapshots, intent basis or fact checks are missing; do not force a positive or negative conclusion.

If repeated observations vary, publish each result and describe the variation. Assess different surfaces separately; a search observation cannot establish AI visibility. Keep “observed effective visibility” distinct from customer action and causal business impact.

## 4. Sampling and independent review

1. **Register scenarios first.** Record audience and intent evidence, inclusion/exclusion rules, surfaces, region/language, exact queries or prompts, time window and planned number of observations. Identify branded, non-branded, comparison and fact-checking queries separately where applicable. Synthetic prompts can illustrate mechanics, but cannot establish real high-value coverage.
2. **Preserve raw evidence.** Save full search results or AI responses, URLs, visible citations, timestamps, model/product labels where available, ad labels and collection conditions. Disclose personalization, login and stochastic limits. If records cannot be public, explain what was redacted and how authorized independent review could occur.
3. **Use two independent reviewers.** Each records item-level decisions and reasoning before discussion. Publish initial agreements, disagreements and resolution based on raw or newly verifiable evidence. A proprietary Omseek score is not an adjudicator. Preserve unresolved disagreements rather than claim consensus.
4. **Report the denominator and missing data.** State registered scenarios, sampled scenarios, observations by surface, omissions/exclusions and reasons, and counts for all four conclusions. A selected case collection must say “not a population estimate.” Do not report illustrative examples as customer outcomes or independent validation.
5. **Reassess changes comparably.** Log intervention, date, affected assets and concurrent changes. Repeat comparable observations where possible. Before/after differences are associations unless the research design supports causal inference.

**Test of reproducibility:** Given the same evidence and rules, an external reviewer should reach the same scenario conclusion or identify the precise ambiguity. Systematic disagreement is a reason to revise this protocol with a versioned record, not to hide counterexamples.

## 5. Illustrative cases — entirely fictional

These invented cases show decisions only. They are **not actual audits, product performance results, or third-party validation**.

### A. Mentioned with an incorrect capability

A fictional small-business user asks for a Shanghai provider of ten-person real-time bilingual video meetings. Supplier A's current site states a two-person limit. An AI answer recommends A as supporting ten people and cites an older third-party page. Preserve full prompt, answer, citation and current first-party specification. Appearance: yes; citation: yes, stale; correct understanding: does not meet; integrity: material factual conflict. Conclusion: **visible, but effectiveness not established**, regardless of mention count.

### B. A ranking for the wrong intent

A fictional procurement manager needs enterprise translation meetings with data retention and audit controls. Supplier B ranks second for “free translation software download,” but its page does not document the required controls and it does not appear in the preregistered procurement query. Preserve both queries. The free-download ranking is real in the hypothetical example, yet it does not establish Effective SEO for this procurement scenario. For the procurement observation: **no visibility observed**; offering fit may separately be **insufficient evidence**.

### C. Relevant and correct, outcomes unknown

A fictional team lead asks whether a ten-person multilingual meeting can be billed per participant-minute. Supplier C has an accessible, current first-party pricing page; an AI answer accurately describes it and links to the page. No click or lead data exist. If intent evidence is documented and no material conflict is known, conclude **evidence-supported effective visibility for this observation**; outcome link is **insufficient evidence**. Do not claim sales impact.

### D. Cropped recommendation screenshot

Only a cropped image saying “Supplier D is best” exists; full prompt, model, date and answer are unavailable. Conclusion: **insufficient evidence**. Keep this state in the record if later evidence permits re-evaluation.

## 6. Reusable scenario record

```yaml
record_id: ""
protocol_version: "draft-0.1"
registered_at: ""
audience_need_and_stage: ""
intent_source_date_and_limitations: ""
intent_status: "supported | plausible-unverified | unknown"
entity_material_claims: ""
owned_asset_urls_and_dates: []
surface: "search | generative_ai"
service_region_language_device: ""
exact_query_or_full_prompt: ""
collection_time_and_conditions: ""
raw_observations: [] # URLs, full snapshots, citations, ad labels
fact_checks_and_counterevidence: []
downstream_evidence_or_unknown: "unknown"
item_judgments: {} # dimension: decision + evidence + counterevidence
scenario_conclusion: ""
reviewer_1_reasoning: ""
reviewer_2_reasoning: ""
disagreements_and_resolution: ""
publication_and_redaction_limits: ""
```

## 7. Publication, boundaries and future validation

A published evaluation should identify the protocol version, sample window and denominator, conclusion counts, exclusions, data gaps and conflicts of interest. Distinguish **founder self-assessment**, **implementation-partner assessment** and **independent external review**. Receiving a contribution is not evidence of endorsement. Framework feedback may use repository Issues; sensitive security reports follow [SECURITY.md](SECURITY.md), not a public Issue.

This public protocol defines checks and evidence. Implementations may retain proprietary intent discovery, composite-score weighting/normalization, confidence algorithms, opportunity ranking, data processing and execution recipes. An implementation's private score is not a universal VGO certification. This protocol neither changes [METRICS.md](METRICS.md) nor declares a public VHI, EVR, VCR or OVR formula. It makes no VCI claim.

Still unvalidated: whether sampled scenarios represent actual high-value intent, whether independent reviewers agree, transfer across services/languages, and any relation between observed effective visibility and business outcomes. A first real pilot should preregister varied intent scenarios, include successes, failures and uncertain results, retain full evidence and have at least two independent reviewers. The pilot succeeds as a methodological test when conclusions can be checked and disagreements exposed; do not set a retrospective “hit rate” target.

Before adoption, compare this draft to the current canonical framework and record the review, any conflicting definitions, and changes in repository history. Revisions should document the contested case, old and new judgment, reason and publication date while preserving historical protocol versions. Until real tests and outside review exist, describe this as a **publicly testable draft**, not a validated industry standard.
