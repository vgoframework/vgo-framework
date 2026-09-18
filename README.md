# VGO Framework

**Visibility Growth Optimization — an open framework for trusted visibility across search, generative AI, and emerging discovery interfaces.**

[![Status](https://img.shields.io/badge/status-v1.0%20draft-orange)](https://github.com/zhangdegit2025/vgo-framework/releases/tag/v1.0.0-draft)
[![License: CC BY 4.0](https://img.shields.io/badge/license-CC%20BY%204.0-blue)](LICENSE)
[![Framework](https://img.shields.io/badge/framework-open-brightgreen)](GOVERNANCE.md)
[![Initiated by Omseek](https://img.shields.io/badge/initiated%20by-Omseek-6C5CE7)](#origin-and-stewardship)

[Official Website](https://vgoframework.org) · [中文说明](README.zh-CN.md) · [Framework](VGO-FRAMEWORK.md) · [Metrics](METRICS.md) · [Integrity & Defense](INTEGRITY-AND-DEFENSE.md) · [Contributing](CONTRIBUTING.md) · [Roadmap](ROADMAP.md)

---

## What is VGO?

**VGO (Visibility Growth Optimization)** is an open methodology for systematically increasing an entity's **trusted visibility, discoverability, understanding, mentions, and citations** across search engines, generative AI systems, answer engines, agents, and emerging discovery interfaces.

SEO optimizes visibility in conventional search systems. GEO focuses on visibility in generative and answer systems. **VGO is the higher-level framework that coordinates both while extending the scope to entity authority, content distribution, technical accessibility, measurement, integrity, and future discovery surfaces.**

> **North Star:** Grow trusted visibility — not visibility at any cost.

## Why VGO?

Discovery is no longer concentrated in a single interface. People and machines increasingly discover brands, organizations, products, people, and knowledge through a mixture of:

- conventional search engines;
- generative AI and answer engines;
- AI assistants and agents;
- third-party publications and citations;
- structured and machine-readable sources;
- vertical and emerging discovery interfaces.

Optimizing each surface in isolation creates fragmented strategy and measurement. VGO provides a common layer for managing **how an entity is discovered, understood, cited, represented, and trusted over time**.

## The VGO model

```text
                         VGO
          Visibility Growth Optimization
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
       SEO                GEO          Emerging Discovery
   Search Visibility   AI Visibility      Agents / Answers
        │                  │                  │
        └──────────────────┼──────────────────┘
                           │
          Entity · Authority · Distribution
          Technical Accessibility · Measurement
                           │
               Visibility Integrity
                & Poisoning Defense
                           │
                  Trusted Visibility
```

### Conceptual model

`Trusted Visibility Growth = Reach × Relevance × Authority × Integrity × Persistence`

This is a conceptual framework, not a universal scientific equation. Implementations should disclose how factors are measured, normalized, sampled, and weighted.

## Seven core pillars

| Pillar | Objective |
| --- | --- |
| **Search Visibility** | Improve discovery, indexing, ranking, snippets, qualified traffic, and search presence. |
| **Generative Visibility** | Improve accurate understanding, mentions, citations, answer inclusion, and contextual presence in AI systems. |
| **Entity & Authority** | Establish canonical identity, consistent facts, evidence, topical authority, and credible corroboration. |
| **Content & Distribution** | Build useful source content and legitimate distribution across owned and third-party channels. |
| **Technical Accessibility** | Improve crawlability, rendering, structured data, machine readability, stable URLs, and performance. |
| **Measurement & Growth** | Establish baselines, visibility shares, experiments, attribution, trends, and business outcomes. |
| **Visibility Integrity & Poisoning Defense** | Detect and respond to misinformation, entity confusion, suspicious sources, manipulation, and provenance failures. |

## Operating loop

```text
Discover → Diagnose → Prioritize → Optimize → Distribute
    ↑                                      ↓
   Learn ← Measure ← Defend ← Verify ←────┘
```

A VGO intervention is not complete when visibility increases. It must also be verified for **accuracy, authority, provenance, integrity, and measurable impact**.

## SEO, GEO, and VGO

VGO does not rename SEO or GEO and does not assume that one strictly depends on the other.

| | SEO | GEO | VGO |
| --- | --- | --- | --- |
| **Primary surface** | Search engines | Generative / answer systems | Cross-surface discovery |
| **Primary goal** | Search visibility | AI mentions, citations, answer inclusion | Trusted visibility growth |
| **Scope** | Search-specific | Generative-system-specific | Strategy, authority, distribution, integrity, measurement |
| **Time horizon** | Continuous | Continuous | Continuous and cross-surface |

See [SEO-GEO-VGO.md](SEO-GEO-VGO.md) for the full relationship model.

## Measurement

VGO separates observable metrics from composite scores. Initial framework metrics include:

**Search Visibility Share · Generative Mention Share · Citation Share · Query/Prompt Coverage · Entity Consistency Rate · Factual Accuracy Rate · Citation Diversity · Integrity Risk · Trusted Visibility Growth Rate**

See [METRICS.md](METRICS.md) for definitions and measurement principles.

## Visibility integrity

Visibility without integrity can become a liability.

VGO treats misinformation, stale facts, entity confusion, malicious content, fabricated consensus, compromised sources, and retrieval/generation manipulation as first-class visibility risks.

The defensive lifecycle is:

**Baseline → Observe → Detect → Verify → Classify → Respond → Revalidate → Recover**

VGO explicitly excludes offensive poisoning, fabricated counter-content, fake reviews, impersonation, hacking, or attempts to bypass third-party safeguards.

See [INTEGRITY-AND-DEFENSE.md](INTEGRITY-AND-DEFENSE.md).

## Documentation

| Document | Purpose |
| --- | --- |
| [VGO-FRAMEWORK.md](VGO-FRAMEWORK.md) | Core framework specification |
| [PRINCIPLES.md](PRINCIPLES.md) | Framework principles |
| [METRICS.md](METRICS.md) | Metrics and measurement model |
| [SEO-GEO-VGO.md](SEO-GEO-VGO.md) | Relationship between SEO, GEO, and VGO |
| [TERMINOLOGY.md](TERMINOLOGY.md) | Common terminology |
| [INTEGRITY-AND-DEFENSE.md](INTEGRITY-AND-DEFENSE.md) | Integrity and defensive framework |
| [RESEARCH-AGENDA.md](RESEARCH-AGENDA.md) | Open research questions |
| [CASE-STUDY-TEMPLATE.md](CASE-STUDY-TEMPLATE.md) | Reproducible case-study format |
| [GOVERNANCE.md](GOVERNANCE.md) | Governance model |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Contribution process |
| [ROADMAP.md](ROADMAP.md) | Framework roadmap |
| [CHANGELOG.md](CHANGELOG.md) | Version history |

## Quick start

If you are evaluating an organization with VGO:

1. Define the entity and canonical facts.
2. Define the relevant search, AI, answer, agent, and discovery surfaces.
3. Establish a reproducible query/prompt baseline.
4. Measure search visibility, generative visibility, citations, entity consistency, authority, and integrity.
5. Diagnose the weakest VGO pillars.
6. Prioritize interventions by expected impact, confidence, effort, and integrity risk.
7. Re-measure using the same sampling protocol.
8. Record uncertainty and avoid claiming causation without evidence.

For formal case documentation, use the [VGO Case Study Template](CASE-STUDY-TEMPLATE.md).

## Origin and stewardship

The **VGO Framework was initiated by Omseek in 2026** and is maintained as an open methodology.

Omseek acts as the founding maintainer. Community proposals, research, corrections, and extensions are welcome through Issues and Pull Requests. Maintainers retain responsibility for release coherence, definitions, governance, and framework integrity.

The open framework is intentionally distinguishable from any specific Omseek product implementation: **VGO is the methodology; Omseek is its initiator, maintainer, and an implementation platform.**

## Cite VGO

GitHub can read the repository's [CITATION.cff](CITATION.cff) metadata. A human-readable citation is:

> VGO Framework. *Visibility Growth Optimization (VGO) Framework*. Version 1.0 Draft, 2026. Initiated by Omseek. https://vgoframework.org

For version-specific references, cite the relevant GitHub release/tag.

## Contributing

VGO is designed to evolve through evidence, reproducible measurement, and open critique—not manufactured consensus.

Read [CONTRIBUTING.md](CONTRIBUTING.md) and [GOVERNANCE.md](GOVERNANCE.md) before proposing framework-level changes.

## License

The framework documentation and methodology are released under **Creative Commons Attribution 4.0 International (CC BY 4.0)**. See [LICENSE](LICENSE).

**Brand rights are separate from the documentation license.** CC BY 4.0 does not by itself grant trademark rights or permission to imply official status, endorsement, certification, sponsorship, or affiliation. See [TRADEMARK.md](TRADEMARK.md).

---

**Current release:** [VGO Framework v1.0.0-draft](https://github.com/zhangdegit2025/vgo-framework/releases/tag/v1.0.0-draft)
