# VGO Framework Public Evaluation Protocol (Draft 0.1)

**Status:** A public draft available for testing. It has not been independently validated and is not a completed specification.  
**Basis:** VGO Framework public definition, frozen baseline V1.0 (2026-09-20).  
**Purpose:** Let evaluators who do not use Omseek make an explainable, reviewable judgment of visibility in a single user-intent scenario, using the same evidence. This document does not define an industry-wide scoring formula and does not claim third-party adoption.

## 1. Scope and boundary

VGO starts from real users and high-value intent. It observes Effective Assets, Effective SEO, Effective GEO, and Effective Visibility, and follows the chain of being discovered, understood, cited, compared, recommended, and chosen. V1 first covers owned assets, search surfaces, and generative AI surfaces. Other surfaces may reuse the record format, but must not be described as validated.

This protocol evaluates **visible evidence in one stated user-intent scenario**. It does not evaluate overall company value, market share, or sales contribution. Search ranking, AI mention, and citation are observations only. Actual user choice and business results need additional first-party evidence. The expression “Right Audience × Right Intent × Right Surface × Right Presence” is not numerical multiplication and must not be used to compute a total score.

Public: the evaluation unit, evidence requirements, judgment rules, disagreement handling, cases, and version history. Remaining inside an implementation: automatic high-value-intent discovery, cross-scenario priority, actual weights / normalization / confidence for VHI and similar indicators, opportunity ranking, automatic execution policy, and commercial data processing. Any implementer may report cases under this public protocol. None may claim that a private score equals a general VGO certification.

## 2. Evaluation unit: one scenario record

Each record must fix the following fields in advance. After observation, the intent and sample must not be rewritten to produce a better-looking result.

| Field | Required content |
|---|---|
| User and question | Target user type, need trigger, concrete question, decision stage; a fabricated low-value question must not be presented as a real need |
| Intent evidence | Source and date from interviews, support/sales records, on-site search, public Q&A, or similar; state source limits. If evidence is missing, mark “unverified intent” |
| Entity and claims | Evaluated entity, product/service, facts to verify, related first-party assets and update dates |
| Surface and query | Search engine or AI service, region/language, device or interface, raw query/prompt and collection time; for AI, record session conditions and any visible model identifier |
| Comparison set | Competitors or other options included in the same scenario, with reasons; do not keep only favorable competitors |
| Observations | Raw result snapshots, links, timestamps, visible position, quoted passages, and citation sources |
| Downstream evidence | If available: source clicks, qualified visits, inquiries, sales quality, and the definition used; do not infer conversion from a screenshot |
| Review record | Evaluators, date, version, judgments and reasons; sensitive data may be redacted, but a reviewable source or access method should remain |

“High value” may be used only as a **reason for choosing the scenario**. State the link to the target user, decision stage, and the organization’s actual offer, and mark whether the evidence is observed, a reasoned assumption, or unknown. This protocol does not supply an algorithm that automatically decides high-value intent, and does not treat “appeared once” as “high-value coverage is complete.”

## 3. Minimum judgment rules

Record each item as `met / not met / insufficient evidence / not applicable`. One good result must not cancel a factual error. Each item must state supporting and contrary evidence. “Met” applies only to **this scenario and this observation**.

| Dimension | Minimum condition for “met” | Common “not met” or insufficient evidence |
|---|---|---|
| Audience and intent | The query reasonably represents the stated user question, and the entity’s offer is relevant to the need | Marketing-invented prompts only; user need not stated; offer is unrelated |
| Owned asset can be verified | Organization-controlled public assets have relevant, checkable facts and an update date or other maintenance clue | No relevant page, page unreachable, key facts missing or stale; having a page is not “Effective Assets” |
| Discovered | The entity or a related asset actually appears in the visible results of the stated surface, with raw evidence kept | Brand-query results used in place of a non-brand scenario; historical results used as this observation |
| Correctly understood | Visible results do not materially distort entity, product, scope, price/limits, or other facts that matter in this scenario | Same-name confusion; a service the organization does not offer; stale price cited; unverifiable facts are insufficient evidence |
| Mention and citation | Distinguish name appearance, content citation, clickable source, and source reliability; keep evidence for each | A mention recorded as a citation; citation cannot be traced or the source is wrong |
| Comparison and recommendation | If comparison/recommendation occurs, judge whether it matches the user need and verified facts; if none occurred, record “not applicable” | Ads, unsupported priority, or a single appearance treated as user choice |
| Integrity risk | Check entity confusion, false/stale facts, suspected poisoning or source conflict, and record the conflicting evidence | A major unresolved conflict still judged “trusted and effective” |
| Outcome link | Report observed business results only when downstream behavior is traceable and definitions are consistent | Exposure, ranking, or mention used in place of clicks, inquiries, closed deals, or incremental contribution |

**Scenario conclusions** use only the following four labels. Do not invent a new index:

- `Evidence-backed Effective Visibility`: audience/intent is relevant, this observation shows visibility, key facts are correct, and no major unresolved integrity risk remains; limited to the observed surface and scenario. Outcome linkage may still be unknown.
- `Visible but effectiveness not established`: it did appear, but the scenario is irrelevant, key facts are wrong, a major integrity risk is unresolved, or an unsupported recommendation is treated as an advantage.
- `Visibility not observed`: it did not appear under the pre-registered query and collection conditions. This does not prove that no users can see it.
- `Insufficient evidence`: complete query conditions, snapshots, scenario basis, or fact-checking material are missing. Do not force a positive or negative conclusion.

If the same scenario is observed more than once, report each run and then describe variation. Do not publish only the best screenshot. Judge each surface separately. Do not treat a search observation as AI visibility.

## 4. Sampling and review protocol

1. **Register the scenario before sampling.** Record the user question and source, inclusion/exclusion rules, surface, region, language, query or prompt, collection window, and expected number of observations. Brand, non-brand, comparison, and verification questions should be presented separately according to the research question. Test prompts without factual basis may be used for a product demo, but they cannot support a “high-value coverage” claim.
2. **Keep raw evidence.** Page URLs, snapshots, and collection time; for search, visible rank and ad labels; for AI, the full prompt, full answer, visible citations, model/product identifier, date, and session conditions. State login, personalization, or randomness limits when they apply. If raw material cannot be published, provide a redacted copy, a hash, or a controlled review method, and state the limits of independent review.
3. **Independent dual coding.** Two evaluators complete the Section 3 judgments and evidence separately, without prior discussion. Record initial agreements and disagreements. Resolve disagreements from raw evidence or newly checkable evidence. Omseek private scores must not decide the outcome. Persistent disagreement is published side by side, not presented as consensus.
4. **Report the denominator and missing cases.** Publish the number of pre-registered scenarios, actual samples, observations per surface, reasons for missing/excluded cases, and counts of the four scenario conclusions. If only cases are shown, mark them clearly as “not a population estimate.” Do not treat a few demo cases as customer results or as validation of the framework.
5. **Observe again after a change.** When an optimization action occurs, record the action, date, affected assets, and unchanged items. Retest with the same scenario and conditions as far as possible, and disclose other concurrent changes. Before/after differences are observational association only. Causal claims need a separate contrast design or stronger evidence.

**Reviewability success condition:** a third party given the same evidence and rules can independently reach the same conclusion or accurately point out an ambiguity in the rules. If systematic disagreement appears, revise the definition and keep the old results. Do not change the standard after the fact to erase counterexamples.

## 5. Worked examples (all fictional; not real investigations or product results)

### Case A: mentioned, but the fact is wrong

Pre-registered scenario: a small-business owner asks how to choose a Shanghai local service that supports real-time two-way translation for a 10-person video meeting. Assume Vendor A’s site says “2 people only.” An AI answer lists it as “supports 10 people” and links to a year-old third-party page. The raw record should include the question, the full answer, the citation, and the current first-party specification.

Judgment: name appearance = `yes`; citation = `present, but the source is stale`; correctly understood = `not met`; integrity risk = `major factual conflict`; scenario conclusion = `Visible but effectiveness not established`. A higher mention count still does not justify “Effective GEO improved.”

### Case B: a search ranking exists, but the user intent does not match

Pre-registered scenario: a procurement manager looks for a real-time translation meeting system that supports enterprise data retention and audit. Assume Vendor B ranks #2 for “free translation software download,” but its product page does not describe retention or audit, and Vendor B is not observed in the pre-registered procurement question. Keep both query results. Do not report only the better ranking.

Judgment: search appearance on the free-tool query = `yes`; relevance to the procurement scenario = `not met or insufficient evidence`; visibility on the procurement question = `Visibility not observed`. An unrelated ranking must not be used to prove “Effective SEO.”

### Case C: relevant and factually correct, conversion unknown

Pre-registered scenario: a multilingual-team lead asks whether a 10-person cross-language meeting can be billed by participant-minute. Assume Vendor C’s site states the pricing clearly, and the AI answer describes it accurately with an accessible first-party source. No click or inquiry data is available.

Judgment: audience/intent, owned asset, discovered, correctly understood, and traceable citation = `met`; no known major conflict. The scenario may be labeled `Evidence-backed Effective Visibility`, and must also state: “this observation only; outcome linkage unknown; do not claim a closed deal.”

### Case D: incomplete record

Only a cropped screenshot saying “AI recommended us first,” with no prompt, model, time, or full answer. Judgment = `Insufficient evidence`. The crop must not enter the numerator of Effective Visibility. After the material is completed, re-evaluate the original scenario and keep the earlier status.

## 6. Reusable single-scenario record template

```yaml
record_id: ""
protocol_version: "VGO-public-evaluation-draft-0.1"
pre_registered_at: ""
audience_and_need: ""
intent_evidence: "source/date/limits or unverified"
decision_stage: ""
entity_and_claims: ""
owned_asset_urls_and_dates: []
surface: "search | generative_ai"
service_region_language_device: ""
query_or_full_prompt: ""
collection_timestamp_and_conditions: ""
observations: [] # raw result URLs, snapshots, full response, citations, ad labels
fact_checks_and_counterevidence: []
downstream_evidence_or_unknown: "unknown"
assessments: # each: met / not met / insufficient evidence / not applicable + evidence
  audience_intent: ""
  owned_asset: ""
  discovered: ""
  correctly_understood: ""
  mentioned_and_cited: ""
  comparison_recommendation: ""
  integrity_risk: ""
  outcome_link: ""
scenario_conclusion: ""
reviewer_a_and_rationale: ""
reviewer_b_and_rationale: ""
disagreements_and_resolution: ""
publication_limits: ""
```

## 7. How results are published, and framework governance

A public case must include at least the protocol version, sampling period, denominator, counts of the four conclusions, missing cases, and any conflict of interest. Distinguish “self-assessment by the methodology initiator,” “implementer assessment,” and “independent third-party review.” External comments must not be described as endorsement of VGO. Public questions may be submitted as a GitHub Issue or through the [contact page](https://www.vgoframework.org/contact). Security issues should use the Security channel on that page. See also [SECURITY.md](SECURITY.md).

The repository filename is `EVALUATION-PROTOCOL.md`, with [examples/README.md](examples/README.md) stating whether examples are fictional or real. Before a revision, maintainers should check [METRICS.md](METRICS.md), [GOVERNANCE.md](GOVERNANCE.md), and [INTEGRITY-AND-DEFENSE.md](INTEGRITY-AND-DEFENSE.md) for conflict. A revision must record the disputed case, the old judgment, the new judgment, the reason, and the publication date. Historical records keep their original protocol version. Commercial ties and evaluator conflicts of interest must be disclosed.

## 8. What remains unvalidated, and first live-pilot acceptance

The following are not yet shown: whether scenario selection represents real high-value intent, agreement across evaluators, transfer across surfaces/languages, and the relationship between Effective Visibility and business results. Private calculations of VHI, EVR, VCR, and OVR are not the validation target of this protocol, and these examples must not be reverse-engineered into a universal formula. VCI is not a formal V1 KPI.

The first live pilot should pre-register at least three intent-scenario types, include success, failure, and insufficient-evidence results, invite at least two independent coders, and keep raw evidence, disagreements, and the full sample as in Section 4. Acceptance looks at whether evaluators can review the work, whether disagreements are explainable, and whether counterexamples change the rules. Do not chase a post-hoc hit-rate target. Until that pilot is complete, this file may only be called a **public evaluation draft available for testing**.

---

**Relation to the frozen baseline:** this file only specifies public judgment and verification. It does not change the VGO definition, add a new first-order theoretical layer or total index, or publish Omseek’s proprietary discovery, scoring, or execution mechanisms.
