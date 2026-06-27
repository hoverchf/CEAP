# ADR-003 Evidence-Driven Analysis

**Status:** Accepted
**Version:** v1.0
**Updated:** 2026-06-27
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Context

Logs are raw data.

Root Cause requires trustworthy evidence instead of assumptions.

The platform must preserve traceability.

---

## Decision

### Evidence is a First-Class Domain Object

Evidence is promoted to a first-class domain object.

Root Cause is defined as:

> A conclusion supported by traceable evidence.

### Evidence Belongs to Analysis Case, Not Session

**Evidence belongs to Analysis Case.**

Sessions consume Evidence but never produce Evidence.

Evidence originates from the real world (tests, captures, experiments), not from analysis activities.

```
Analysis Case
    ├── Evidence (owned by Case)
    │
    └── Analysis Session
            ├── Consumes Evidence
            └── May generate Evidence Requests
                    ↓
            Investigation (real-world activity)
                    ↓
            New Evidence → added to Case
```

Evidence is continuously growing across the life of a Case.
Multiple Sessions may share the same Evidence.

### Evidence Sources

Evidence may originate from:

- Android Log
- Modem Log
- Network Log
- Video
- Metrics
- Test Report
- External Analysis
- CPU Profile
- PCAP
- Screenshots
- Configuration

### Four-Type Classification

All domain objects must belong to exactly one of four types:

| Type | Objective? | Example |
|------|-----------|---------|
| **Evidence** | Yes | RTT=20ms, Log, Video, PCAP |
| **Observation** | No | RTT is normal, retransmission rate is slightly high |
| **Finding** | No | Network has slight packet loss |
| **Decision** | No | Capture Server Log, close Case |

**Evidence = Facts**
**Observation = Interpretation of facts**
**Finding = Reasoning conclusion**
**Decision = Next action**

These four layers must never be conflated.

### Evidence → Observation → Finding Chain

```
Evidence
    ↓
Observation
    ↓
Hypothesis
    ↓
Reasoning
    ↓
Finding
    ↓
Root Cause
    ↓
Decision (next action or case closure)
```

---

## Principle

Root Cause is not an answer.

Root Cause is an evidence-supported conclusion.

Evidence must never be mixed with Observation, Finding, or Decision.

---

## Consequences

1. Future AI capabilities must explain reasoning using evidence.
2. Evidence traceability is a mandatory platform capability.
3. Evidence storage and management is a Case-level concern, not a Session-level concern.
4. Session design must enforce: consume Evidence only, never modify Evidence.
5. Investigation is the bridge between Session output (Decision) and new Evidence input.

---

## Cross-References

- **ADR-001** — Evidence belongs to Case; Session consumes Evidence
- **ADR-002** — Reasoning uses Evidence as input
- **B-001** — Four-Type Classification formalizes Evidence vs Observation vs Finding
- **CM-002** — Evidence is a peer of Investigation and Session under Case
- **CM-003** — Ubiquitous Language provides strict definitions of Evidence, Observation, Finding
- **VF-001** — Evidence quality maps to Quality Value
- **WF-001** — This ADR follows the Architecture Decision Record guidelines
