# ADR-002 Reasoning Framework

Status

Accepted

---

## Context

Different communication scenarios require different expert reasoning processes.

Recursive reasoning is only one possible strategy.

The platform must remain extensible.

---

## Decision

CEAP defines a generic Reasoning Framework.

The framework is independent of any specific reasoning model.

Different domains may register different Reasoning Models.

Examples include:

- Recursive Narrowing
- Timeline Reconstruction
- Rule-based Reasoning
- Decision Tree
- Pattern Matching
- Protocol State Machine
- LLM Guided Reasoning

---

## Principle

The platform is reasoning-model agnostic.

Reasoning Models are pluggable strategies instead of platform architecture.

---

## Consequences

Adding new communication domains should only require new Reasoning Models.

No architecture redesign should be necessary.