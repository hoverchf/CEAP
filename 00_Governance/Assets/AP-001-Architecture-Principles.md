# AP-001 Architecture Principles

**Status:** Approved
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Purpose

Architecture Principles define the highest-level design rules of CEAP.

All future assets shall comply with these principles.

---

## 1. Knowledge First

```
Knowledge
    ↓
Methodology
    ↓
SDK
    ↓
Tool
    ↓
AI Agent
```

---

## 2. Everything is Versioned

Everything has versions.

---

## 3. Repository is the Single Source of Truth

Repository stores approved assets only.

---

## 4. Methodology Before Automation

Methodology always precedes automation.

---

## 5. Generalize Before Implement

```
Knowledge
    ↓
SDK
    ↓
Skill
    ↓
Tool
    ↓
Implementation
```

---

## 6. Architecture Before Repository

Architecture defines Repository.

Never the opposite.

---

## 7. Workshop Driven Evolution

```
Workshop
    ↓
Review
    ↓
Architecture Freeze
    ↓
Deliverable
    ↓
Repository
```

---

## 8. Evidence Driven Analysis

```
Observation
    ↓
Evidence
    ↓
Hypothesis
    ↓
Validation
    ↓
Root Cause
```

---

## 9. Reusable Knowledge over One-time Solution

Every analysis should become reusable knowledge.

---

## 10. Human Expert Remains in Control

AI augments experts.

Experts make final decisions.

---

## 11. Progressive Narrowing

```
Problem
    ↓
Stage
    ↓
Evidence
    ↓
Hypothesis
    ↓
Validation
    ↓
Root Cause
```

> **Note:** Principle 8 and Principle 11 describe complementary views of the same analysis process. Principle 8 focuses on the evidential foundation (Observation → Evidence), while Principle 11 focuses on the progressive scoping (Problem → Stage). Both are valid and serve different abstraction levels.

---

## 12. Platform over Project

Always build platform capability.

---

## 13. Knowledge and Engineering Separation

Knowledge must remain independent from implementation.

---

## Architecture Decisions

> **Note:** Decision IDs D-009 through D-015 were originally recorded in Workshop session-3.md and are canonically declared here.

| ID | Decision | Status |
|----|----------|--------|
| D-009 | Enterprise Capability First | Frozen |
| D-010 | Expertise is the Source | Frozen |
| D-011 | Knowledge as Enterprise Asset | Frozen |
| D-012 | Evidence Before Conclusion | Frozen |
| D-013 | Platform Amplifies Experts | Frozen |
| D-014 | Architecture Evolves Incrementally | Frozen |
| D-015 | Architecture Assets are the Single Source of Truth | Frozen |

---

## Cross-References

- **VF-001** Value Framework — All value creation must comply with these principles
- **FP-001** CEAP Definition — This definition is constrained by these principles
- **WF-001** Architecture Workflow — Principles guide asset production and governance
- **CM-002** Core Concept Model — Concepts are designed to satisfy these principles
