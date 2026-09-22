# VGO Metrics 1.0

**Version:** [v1.0.0-draft](https://github.com/vgoframework/vgo-framework/releases/tag/v1.0.0-draft)

## 1. Measurement principle

VGO separates **raw exposure**, **Effective Visibility**, and **business outcomes**.

A measurement system should not assume that every query, prompt, ranking, mention, citation, or discovery opportunity has equal value.

Measurement should begin with a defined population of users, needs, intents, problem spaces, and relevant Visibility Surfaces.

## 2. What should be observed

A VGO measurement program may observe:

- discovery and coverage across relevant search, answer, and generative contexts;
- question coverage, answer eligibility, answer presence, answer selection, answer share, and answer-source attribution;
- relevance to real user needs and high-value intent;
- accuracy and consistency of entity facts;
- source quality, authority, corroboration, and citation diversity;
- presence in understanding, comparison, recommendation, and selection contexts;
- first-party asset coverage and maintainability;
- downstream observable outcomes where appropriate;
- integrity risks, conflicting claims, and provenance issues;
- change over time using comparable sampling.

## 3. Capability-domain metrics

SEO, AEO, and GEO require related but non-identical observations:

- **SEO** may measure crawl/index eligibility, qualified ranking visibility, search-result presence, result type, clicks, and downstream behavior where observable.
- **AEO** may measure question coverage, answer completeness, extraction readiness, answer presence, answer selection, answer share, provenance, accuracy, consistency, and freshness across declared Answer Surfaces.
- **GEO** may measure entity understanding, mention quality, citation/reference presence, source diversity, comparison inclusion, recommendation/selection, and cross-run stability across declared generative surfaces.

An implementation must declare its surface taxonomy, eligible sample set, time window, exclusions, and uncertainty. A raw extraction, mention, or citation must not be presented as verified value by itself.

## 4. Effective Visibility

Conceptually:

**Effective Visibility = Right Audience × Right Intent × Right Surface × Right Presence**

This model communicates the logic of Effective Visibility. It is **not** a universal mathematical equation and should not be presented as a fixed scientific scoring formula.

Single-scenario public judgments follow [EVALUATION-PROTOCOL.md](EVALUATION-PROTOCOL.md). That draft does not turn this model into a total score.

## 5. Measurement quality

Implementations should document, where practical:

- what population or audience is being evaluated;
- which intents or problem spaces are included;
- which Visibility Surfaces are sampled;
- the sampling period and frequency;
- how observations are normalized or compared;
- known uncertainty and data limitations.

## 6. Outcomes and attribution

Where first-party analytics are available, organizations may observe traffic, engagement, key-page behavior, leads, conversions, or other outcomes.

These signals improve observability but do not create perfect causal attribution. Multi-touch, cross-device, opaque search systems, and opaque AI systems can prevent deterministic claims.

## 7. Composite indices

Composite indices can be useful for diagnosis and communication, but the VGO Framework does not require one universal public score.

Any composite score should disclose enough about its conceptual dimensions and limitations to be interpretable. Commercial implementations may use proprietary models.

## 8. Public / proprietary boundary

The open VGO Framework defines **measurement principles and conceptual standards**.

It intentionally does **not** publish:
- proprietary scoring weights;
- normalization formulas;
- intent-discovery algorithms;
- high-value scoring logic;
- opportunity-prioritization algorithms;
- automation rules;
- commercial diagnosis recipes;
- implementation-specific competitive intelligence methods.

This boundary allows the methodology to remain open while implementations can develop differentiated technology and operational systems.
