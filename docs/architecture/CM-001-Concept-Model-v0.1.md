# CM-001 Concept Model v0.1

**Status:** Deprecated
**Replaced by:** CM-002 Core Concept Model
**Deprecated:** 2026-06-27

---

> This concept model has been superseded by CM-002.
>
> Key changes:
> - Platform core object changed from Analysis Session to **Analysis Case**
> - **Investigation** introduced as independent domain object
> - **Observation** separated from Evidence and Finding
> - **Hypothesis** recognized as connecting Evidence and Reasoning
> - Full domain model now includes: Case, Session, Evidence, Investigation, Observation, Finding, Hypothesis, Root Cause, Knowledge Assets

---

## Enterprise View

```
Expertise
    ↓
Analysis Session
    ↓
Knowledge Assets
    ↓
Enterprise Capability
```

---

## Core Domain Objects

### Analysis Session

The primary managed object.

Contains one complete expert analysis.

---

### Reasoning Model

Defines how an Analysis Session performs reasoning.

Reasoning Models are replaceable.

---

### Evidence

Evidence supports observations, hypotheses and conclusions.

Evidence is traceable.

---

### Knowledge Assets

Produced from completed Analysis Sessions.

Examples:

- SOP
- Pattern
- Rule
- Case
- Checklist
- Stage Definition

---

## Architecture Principles

Expertise is the source.

Knowledge Assets are the carrier.

Platform is the amplifier.

Enterprise Capability is the goal.

Analysis Session is the primary vehicle for transforming expertise into enterprise knowledge.

The platform is reasoning-model agnostic.

Root Cause must always be supported by evidence.
