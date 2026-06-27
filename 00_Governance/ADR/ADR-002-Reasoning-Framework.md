# ADR-002 Reasoning Framework

**Status:** Accepted
**Version:** v1.0
**Updated:** 2026-06-27
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Context

Different communication scenarios require different expert reasoning processes.

Recursive reasoning is only one possible strategy.

The platform must remain extensible.

---

## Decision

### CEAP Defines a Generic Reasoning Framework

CEAP defines a generic Reasoning Framework.

The framework is independent of any specific reasoning model.

Different domains may register different Reasoning Models.

**Examples of Reasoning Models:**

- Recursive Narrowing
- Timeline Reconstruction
- Rule-based Reasoning
- Decision Tree
- Pattern Matching
- Protocol State Machine
- LLM Guided Reasoning

### Session Purpose is Reducing Uncertainty

A Session's purpose is not to find Root Cause.

A Session's purpose is to **reduce uncertainty** (reduce problem space).

Sometimes a Session may only:

- Exclude "Server"
- Exclude "Network"
- Suspect "Client"

This Session is still successful because the problem space has shrunk.

Some Sessions do not exclude any module, but increase confidence in a hypothesis.
This also reduces uncertainty.

### Session Success Criteria

A Session creates value if it achieves **any** of the following:

- Adds valid Evidence
- Excludes a hypothesis
- Discovers a new hypothesis
- Shrinks the problem space
- Validates an existing conclusion
- Forms new knowledge

Root Cause is only the cumulative result of many Sessions, not the goal of each Session.

### Reasoning Model is CEAP's Differentiator

The Reasoning Model is what distinguishes CEAP from other platforms.

While Case, Session, and Evidence are relatively stable, the Reasoning Model determines:

- How uncertainty is reduced
- How hypotheses evolve
- How AI assists expert judgment

Future AI capabilities must explain reasoning using evidence.

Evidence traceability becomes a mandatory platform capability.

---

## Principle

The platform is reasoning-model agnostic.

Reasoning Models are pluggable strategies, not platform architecture.

---

## Consequences

1. Adding new communication domains should only require new Reasoning Models.
2. No architecture redesign should be necessary for new domains.
3. Future AI capabilities must be reasoning-model aware.
4. Reasoning Model design is the highest-leverage architecture activity for CEAP.

---

## Cross-References

- **CM-002** — Reasoning Models operate within Analysis Sessions
- **CM-003** — Ubiquitous Language defines Session, Hypothesis, and Evidence
- **ADR-001** — Sessions belong to Cases; Reasoning Models reduce uncertainty within Sessions
- **ADR-003** — Evidence supports reasoning; traceability is mandatory
- **B-001** — Four-Type Classification constrains what reasoning can produce
- **VF-001** — Reasoning quality maps to Quality Value and Knowledge Value
- **WF-001** — This ADR follows the Architecture Decision Record guidelines
