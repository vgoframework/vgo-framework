# VGO Metrics 1.0

**Reading copy:** https://www.vgoframework.org/docs/metrics  
**Version:** [v1.0.0-draft](https://github.com/vgoframework/vgo-framework/releases/tag/v1.0.0-draft)

VGO deliberately separates **raw metrics** from **qualified/effective visibility** and from any **composite model**.

A measurement system should not assume that every query, prompt, mention or discovery opportunity has equal value. Sampling should reflect real user needs and relevant decision contexts where practical.

The framework defines what should be measured conceptually; it does not prescribe a universal commercial scoring recipe, fixed weighting model or implementation algorithm.

## Visibility
- Search Visibility Share (SVS)
- Generative Mention Share (GMS)
- Citation Share (CS)
- Query/Prompt Coverage (QPC)
- Qualified Discovery Reach (QDR)

## Intent & relevance
- High-Value Problem Space Coverage (HPSC)
- Intent-Relevant Visibility Rate (IRVR)
- Contextual Relevance Rate (CRR)

These metrics are conceptual categories. What constitutes a high-value problem space or qualified intent depends on the entity, audience and use case and should be documented by each implementation.

## Quality & authority
- Source Authority Mix (SAM)
- Citation Diversity (CD)
- Entity Consistency Rate (ECR)
- Factual Accuracy Rate (FAR)

## Integrity
- Poisoning/Anomaly Incidence (PAI)
- Untrusted Source Exposure (USE)
- False/Conflicting Claim Rate (FCR)
- Mean Time to Detect (MTTD)
- Mean Time to Correct/Recover (MTTC/R)

## Growth & outcomes
- Visibility Growth Rate (VGR)
- Trusted Visibility Growth Rate (TVGR)
- Visibility-to-Outcome Conversion (VOC)

Where first-party analytics are available, implementations may also observe traffic sources, content engagement, key-page behavior and conversion trends. These signals improve observability but should not be presented as perfect causal attribution, especially across multi-touch or cross-device journeys.

## Conceptual composite

`TVG = Reach × Relevance × Authority × Integrity × Persistence`

Do not present this conceptual equation as a universal scientific constant. Implementations may operationalize these dimensions differently and should document enough methodology for results to be interpretable and comparable.

The VGO Framework intentionally does not define proprietary weighting, prioritization, intent-discovery or automation algorithms.
