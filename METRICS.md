# VGO Metrics 1.0

**Version:** VGO Framework V1.0 published methodology ([release notes](docs/RELEASE-NOTES-V1.0.md)); public evaluation protocol Draft 0.1 remains separately scoped.

## 1. Measurement serves action and verification

VGO is an action framework. Metrics help diagnose gaps, prioritize interventions, verify comparable observations and update the next action plan; a score alone is not an execution plan or an outcome. Report the scenario, action, affected asset, observation window, uncertainty and contrary evidence when evaluating change.

**Outcome levels:** (1) answer and search signals, such as mentions and citations; (2) scenario-bound evidence-backed Effective Visibility, including relevant intent, accuracy and integrity; (3) observed user choice or business results, which require additional downstream evidence. Do not promote a level (1) signal into level (2) or (3) without evidence. Cross-surface longitudinal growth requires repeated, comparable observations and must not be inferred from the public single-scenario protocol alone.

## 2. Measurement principle

VGO separates **raw exposure**, **Effective Visibility**, and **business outcomes**.

A measurement system should not assume that every query, prompt, ranking, mention, citation, or discovery opportunity has equal value.

Measurement should begin with a defined population of users, needs, intents, problem spaces, and relevant Visibility Surfaces.

## 3. What should be observed

A VGO measurement program may observe:

- discovery and coverage across relevant search, direct-answer and generative contexts;
- direct-answer eligibility, observed presence, factual accuracy and traceable source support, with eligibility and presence recorded separately;
- relevance to real user needs and high-value intent;
- accuracy and consistency of entity facts;
- source quality, authority, corroboration, and citation diversity;
- presence in understanding, comparison, recommendation, and selection contexts; when an AI answer is assessed under both AEO and GEO, identify the shared observation and avoid double counting;
- first-party asset coverage and maintainability;
- downstream observable outcomes where appropriate;
- integrity risks, conflicting claims, and provenance issues;
- change over time using comparable sampling.

AEO observations should record the exact question, surface, time, answer text and source links where available; distinguish no answer, an answer without the entity, an accurate entity answer, and an inaccurate or unsupported entity answer. Do not infer eligibility from one absent answer, or user choice from answer presence. Where eligibility is unobservable, report it as unknown rather than estimating a precise rate. See [the capability comparison](SEO-GEO-VGO.md).

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

VHI, EVR, VCR and OVR may appear in private implementation discussions, but are not four mandatory public VGO indices or validated targets of the single-scenario public protocol. This boundary allows the action framework to remain open while implementations can develop differentiated technology and operational systems.
