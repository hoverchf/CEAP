# B-001 Investigation & Four-Type Classification

**Status:** Frozen
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## 1. Discovery Context

This asset formalizes two major architectural discoveries from Workshop Session-007 and Session-008.

Both discoveries fundamentally reshape the domain model by separating concerns that were previously conflated.

---

## 2. B-001: Investigation as Independent Domain Object

### Problem

Previously we modeled:

```
Analysis Case
    ├── Evidence Collection
    └── Analysis Session
```

**Evidence Collection** emphasizes action. But in reality, what happens is:

> "Go investigate the Server." or "Get a CPU Profile." or "Run another test."

The business concept is **Investigation**, not Evidence Collection.

### Correct Model

```
Analysis Case
    ├── Investigation
    │       └── produces
    │
    ├── Evidence
    │       └── is the result of Investigation
    │
    └── Analysis Session
            └── explains Evidence
```

**Key insight:**

- **Investigation** is not analysis. It is data acquisition.
- **Evidence** is not analysis. It is the result.
- **Analysis Session** is where analysis happens.

### Relationship to Real World

```
Session
    ↓
Investigation Request
    ↓
Investigation (real-world activity)
    ↓
New Evidence
    ↓
New Session
```

Evidence comes from the real world (tests, captures, experiments), not from analysis activities.

### Revised Principle

> **Analysis Session consumes Evidence and may generate Evidence Requests, but it never produces Evidence.**

### Updated Case Model

```
Analysis Case
    ├── Investigation
    ├── Evidence
    ├── Analysis Session
    ├── Observation
    ├── Finding
    ├── Root Cause
    └── Knowledge Assets
```

---

## 3. B-001: Four-Type Classification

### Problem

Previous analysis reports mixed four distinct concepts:

- Evidence (facts)
- Observation (interpretations)
- Finding (conclusions)
- Decision (actions)

This confusion prevents AI from learning correctly.

### Classification

| Type | Objective? | Example |
|------|-----------|---------|
| **Evidence** | Yes — objective fact | RTT=20ms, Log, Video, PCAP |
| **Observation** | No — human interpretation | RTT is normal, retransmission rate is slightly high |
| **Finding** | No — reasoning conclusion | Network has slight packet loss |
| **Decision** | No — next action | Capture Server Log, close Case |

### Real Example

```
Evidence: TCP Retransmission = 3%
    ↓
Observation: Retransmission rate is slightly elevated
    ↓
Finding: Network has minor packet loss
    ↓
Root Cause: WiFi AP anomaly
```

These four layers must never be conflated.

### Distinction Between Observation and Finding

- **Observation** = what the expert sees when looking at Evidence
- **Finding** = what the expert concludes after Reasoning

---

## 4. Revised Reasoning Flow

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

## 5. Architecture Decisions

> **Note:** Decision IDs D-027 through D-030 are canonically declared in **CM-002** (Core Concept Model). This table is retained for historical traceability. For authoritative declarations, see CM-002 §5.

| ID | Decision | Status |
|----|----------|--------|
| D-027 | Investigation is an independent domain object, not part of Analysis Session | Frozen |
| D-028 | Session consumes Evidence but never produces Evidence | Frozen |
| D-029 | Four-Type Classification (Evidence/Observation/Finding/Decision) is mandatory for all domain objects | Frozen |
| D-030 | Investigation bridges Session output (Decision) and new Evidence input | Frozen |

---

## Cross-References

- **CM-002** — Investigation and Four-Type Classification are integrated into the full concept model
- **CM-003** — Each of the four types has a strict definition
- **ADR-001** — Case structure includes Investigation
- **ADR-003** — Evidence belongs to Case, consumed by Session
- **WF-001** — This is a B-type discovery formalized as a Frozen asset
