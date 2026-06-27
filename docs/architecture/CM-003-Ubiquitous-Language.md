# CM-003 Ubiquitous Language

**Status:** Freeze Candidate
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Purpose

This document establishes the **Ubiquitous Language** for CEAP.

Every term defined here has a single, precise meaning.

All future assets (PC-001, Vision, Architecture, Domain Model, AI Agent, Database, API) must use these terms consistently.

Once frozen, this language becomes the reference for all CEAP communication.

---

## Core Terms

### Analysis Case

**Definition:** The core business object managed by CEAP.

Represents one complete business problem lifecycle, from problem discovery to final resolution and knowledge extraction.

**Rules:**

- One business problem = one Case
- A Case can contain unlimited Analysis Sessions
- A Session belongs to exactly one Case
- Knowledge Assets belong to the Case, not individual Sessions
- Root Cause can evolve; no requirement for first-session certainty

**Not:**

- A single log file
- A single analysis activity
- A report

---

### Analysis Session

**Definition:** One complete analysis activity conducted by an expert (or AI) around an Analysis Case.

**Rules:**

- A Session is an analysis activity, not a business object
- A Session's purpose is to reduce uncertainty
- A Session does not necessarily output Root Cause
- A Session can involve one expert, multiple experts, AI, or AI + expert
- A Session is not bound to personnel; it is bound to analysis activity
- A Session is CEAP's smallest analysis recording unit

**Not:**

- A business problem
- A Root Cause
- A report

---

### Investigation

**Definition:** A real-world activity initiated to acquire new Evidence.

**Rules:**

- Investigation is not analysis; it is data acquisition
- Investigation is triggered by Session output (Decision)
- Investigation produces Evidence (added to Case)
- Evidence comes from the real world (tests, captures, experiments), not from analysis

**Examples:**

- "Capture CPU Profile"
- "Run another test"
- "Get Server Log"

**Not:**

- An analysis activity
- A tool action

---

### Evidence

**Definition:** Objective facts that support the analysis.

**Rules:**

- Evidence is objective fact (not interpretation, not conclusion)
- Evidence belongs to Analysis Case, not to any single Session
- Evidence is continuously growing throughout the Case lifecycle
- Multiple Sessions may share the same Evidence
- A Session consumes Evidence but never modifies or produces Evidence

**Types:**

- Log, Trace, PCAP, Video, Counter, Configuration, Test Result, Screenshot, AI Analysis Result

**Not:**

- An observation
- A finding
- A conclusion

---

### Observation

**Definition:** An expert's interpretation of Evidence.

**Rules:**

- Observation is not a fact; it is a human interpretation of facts
- Observation depends on the observer's expertise
- The same Evidence may produce different Observations from different experts

**Not:**

- Evidence (fact)
- Finding (conclusion)

---

### Hypothesis

**Definition:** A tentative explanation proposed to account for observed phenomena.

**Rules:**

- Hypotheses connect Evidence/Observation with Reasoning
- A Case may have multiple concurrent hypotheses
- Sessions may add, update, or eliminate hypotheses
- Hypothesis elimination is itself a value-creating Session outcome

**Not:**

- A confirmed finding
- A Root Cause

---

### Finding

**Definition:** A conclusion reached after reasoning, supported by evidence and observations.

**Rules:**

- Finding is not an observation; it is a reasoned conclusion
- Finding requires evidence traceability
- Finding is more definitive than Observation

**Not:**

- An observation
- Raw evidence

---

### Root Cause

**Definition:** A conclusion supported by traceable evidence, representing the fundamental cause of the problem.

**Rules:**

- Root Cause is not an answer; it is an evidence-supported conclusion
- Root Cause can evolve across Sessions
- Root Cause is not the final output of a Case; Knowledge Assets are

**Not:**

- An assumption
- A guess
- A one-session conclusion

---

### Knowledge Assets

**Definition:** Reusable knowledge produced from completed Analysis Cases.

**Rules:**

- Knowledge Assets belong to the Case, not individual Sessions
- They are the Case's final value output
- They represent the transformation from expertise to enterprise capability

**Examples:**

- SOP, Pattern, Rule, Case, Checklist, Stage Definition, Evidence Pattern, Root Cause Pattern, Expert Experience, Workflow

**Not:**

- A one-time Root Cause
- Temporary analysis notes

---

## Four-Type Classification

All domain objects must belong to exactly one of these four types:

| Type | Objective? | Example |
|------|-----------|---------|
| **Evidence** | Yes | RTT=20ms, Log, Video, PCAP |
| **Observation** | No | RTT is normal, retransmission rate is slightly high |
| **Finding** | No | Network has slight packet loss |
| **Decision** | No | Capture Server Log, close Case |

**Rule:** Any object that cannot be classified into one of these four types requires re-evaluation.

---

## Analysis Flow

```
Analysis Case
    ├── Investigation → produces Evidence
    ├── Analysis Session
    │       ├── consumes Evidence
    │       ├── produces Observation
    │       ├── generates Hypothesis
    │       ├── produces Finding
    │       └── produces Decision
    │               └── may trigger Investigation
    ├── Root Cause (evolves across Sessions)
    └── Knowledge Assets (final output)
```

---

## Cross-References

- **ADR-001** — Analysis Case as core domain object
- **ADR-002** — Reasoning Framework operates within Sessions
- **ADR-003** — Evidence-driven analysis with traceability
- **B-001** — Investigation and Four-Type Classification
- **CM-002** — Core Concept Model (structural relationships)
- **VF-001** — All terms serve the Value Framework
- **FP-001** — This language implements the Core Transformation
- **WF-001** — Terminology governance follows this workflow
