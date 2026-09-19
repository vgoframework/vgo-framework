# Visibility Integrity & Poisoning Defense

**Reading copy:** https://www.vgoframework.org/docs/integrity-and-defense  
**Version:** [v1.0.0-draft](https://github.com/vgoframework/vgo-framework/releases/tag/v1.0.0-draft)


## Objective
Protect the accuracy, provenance and trustworthiness of an entity's representation across search and AI discovery systems.

## Threat model
VGO monitors risks such as:
- false or misleading claims about an entity;
- entity confusion, impersonation or misattribution;
- low-quality duplicated content overwhelming higher-quality sources;
- malicious or coordinated content intended to distort retrieval or generated answers;
- compromised first-party pages or unauthorized changes;
- stale facts continuing to propagate after official information changes;
- fabricated citations, reviews, endorsements or consensus;
- prompt-injection-like instructions embedded in content intended to manipulate downstream automated systems.

## Defensive lifecycle
**Baseline → Observe → Detect → Verify → Classify → Respond → Revalidate → Recover**

### Baseline
Maintain canonical facts, official URLs, entity identifiers, approved claims and high-confidence source references.

### Observe
Sample search results, AI answers, citations, media mentions and relevant third-party sources over time.

### Detect
Flag unusual changes in source mix, claim frequency, entity attributes, citation domains, sentiment-independent factual conflicts and sudden visibility spikes.

### Verify
Do not label disagreement as poisoning automatically. Compare claims against provenance, timestamps, primary evidence and multiple credible sources.

### Respond
Prefer legitimate corrective actions: update first-party evidence, request corrections where appropriate, publish transparent clarifications, repair compromised assets, improve structured/canonical signals and strengthen reputable corroboration.

### Recover
Track whether inaccurate claims and untrusted-source exposure decline and whether correct canonical information returns across discovery surfaces.

## Guardrails
VGO defense must not become offensive manipulation. It excludes hacking, harassment, fabricated counter-content, fake reviews, deceptive identity tactics, poisoning competitors, or attempts to bypass third-party safeguards.

## Integrity scoring
Implementations may calculate an Integrity Score from factual consistency, provenance quality, source trust, anomaly incidence and recovery state. Exact scoring must be documented; uncertainty should remain visible.
