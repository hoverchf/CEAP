# CM-002 Core Concept Model

**Status:** Freeze Candidate
**Version:** v1.0
**Replaces:** CM-001 (Deprecated)
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## 1. Enterprise View

```
Expertise
    ↓
Knowledge Assets
    ↓
Platform
    ↓
Enterprise Capability
```

This is CEAP's core architecture principle.

No design may violate this value chain.

---

## 2. Top-Level Domain Model

```
Analysis Case
    ├── Metadata
    ├── Problem Description
    ├── Investigation(s)
    │       └── produces →
    ├── Evidence
    │
    ├── Analysis Session(s)
    │       ├── consumes → Evidence
    │       └── produces →
    │           ├── Observation
    │           ├── Finding
    │           ├── Hypothesis
    │           └── Decision (→ triggers Investigation)
    │
    ├── Root Cause
    │
    └── Knowledge Assets
```

---

## 3. Core Concepts

### 3.1 Analysis Case

**Definition:** The core business object managed by CEAP.

An Analysis Case represents one complete business problem lifecycle, from problem discovery to final resolution and knowledge extraction.

**Key properties:**

- One business problem = one Case
- A Case can contain unlimited Analysis Sessions
- A Session belongs to exactly one Case
- Knowledge Assets belong to the Case, not individual Sessions
- Root Cause can evolve; no requirement for first-session certainty
- Knowledge Assets are the Case's final value output

**Lifecycle:**

```
Problem Report
    ↓
Case Created
    ↓
Evidence Collection (via Investigation)
    ↓
Multiple Analysis Sessions
    ↓
Hypothesis Evolution
    ↓
Root Cause Confirmation
    ↓
Knowledge Extraction
    ↓
Case Closed
```

---

### 3.2 Analysis Session

**Definition:** One complete analysis activity conducted by an expert (or AI) around an Analysis Case.

A Session describes an **analysis activity**, not a business problem, not a Root Cause, not a report.

**Key properties:**

- A Session is part of a Case, not a top-level platform object
- A Session's purpose is to **reduce uncertainty** (reduce problem space)
- A Session does not necessarily output Root Cause
- A Session can be conducted by one expert, multiple experts, AI, or AI + expert
- A Session is not bound to personnel; it is bound to analysis activity
- Each Session must be independently recordable, replayable, and auditable
- A Session is CEAP's smallest analysis recording unit

**Session success criteria (any one is sufficient):**

- Adds valid Evidence
- Excludes a hypothesis
- Discovers a new hypothesis
- Shrinks the problem space
- Validates an existing conclusion
- Forms new knowledge

**Session lifecycle:**

```
Session Start
    ↓
Consume Evidence
    ↓
Generate / Update Hypothesis
    ↓
Reasoning
    ↓
Validation
    ↓
Session Result
    ↓
Next Session (Optional)
```

**Session output:**

- Observation
- Finding
- Hypothesis
- Validation Result
- Elimination Result
- Next Investigation Request

---

### 3.3 Investigation

**Definition:** A real-world activity initiated to acquire new Evidence.

Investigation is the bridge between Session output (Decision) and new Evidence input.

**Key properties:**

- Investigation is not analysis; it is data acquisition
- Examples: capture CPU Profile, run another test, get Server Log
- Investigation is triggered by Session output (Decision)
- Investigation produces Evidence (added to Case)
- Evidence comes from the real world, not from analysis activities

**Relationship:**

```
Session → Decision (e.g., "Capture Server Log")
    ↓
Investigation Request
    ↓
Investigation (real-world activity)
    ↓
New Evidence → added to Case
    ↓
New Session begins
```

---

### 3.4 Evidence

**Definition:** Objective facts that support the analysis.

Evidence belongs to Analysis Case, not to any single Session.

**Key properties:**

- Evidence is objective fact (not interpretation, not conclusion)
- Evidence is continuously growing throughout the Case lifecycle
- Multiple Sessions may share the same Evidence
- A Session consumes Evidence but never modifies or produces Evidence
- Evidence may originate from: Log, Trace, PCAP, Video, Counter, Configuration, Test Result, Screenshot, AI Analysis Result

**Sources:**

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

---

### 3.5 Observation

**Definition:** An expert's interpretation of Evidence.

Observation is the bridge between Evidence and Reasoning.

**Key properties:**

- Observation is not a fact; it is a human interpretation of facts
- Observation depends on the observer's expertise
- The same Evidence may produce different Observations from different experts

**Example:**

```
Evidence: TCP Retransmission = 3%
    ↓
Observation: Retransmission rate is slightly elevated
```

---

### 3.6 Hypothesis

**Definition:** A tentative explanation proposed to account for observed phenomena.

Hypothesis connects Evidence/Observation with Reasoning.

**Key properties:**

- Hypotheses evolve across Sessions
- A Case may have multiple concurrent hypotheses
- Sessions may add, update, or eliminate hypotheses
- Hypothesis elimination is itself a value-creating Session outcome

**Evolution:**

```
Evidence → Observation → Hypothesis → New Evidence → Hypothesis Update → Hypothesis Elimination → Root Cause
```

---

### 3.7 Finding

**Definition:** A conclusion reached after reasoning, supported by evidence and observations.

**Key properties:**

- Finding is not an observation; it is a reasoned conclusion
- Finding requires evidence traceability
- Finding is more definitive than Observation

**Example:**

```
Observation: Retransmission rate is slightly elevated
    ↓
Reasoning: Elevated retransmission causes latency
    ↓
Finding: Network has minor packet loss
```

---

### 3.8 Root Cause

**Definition:** A conclusion supported by traceable evidence, representing the fundamental cause of the problem.

**Key properties:**

- Root Cause is not an answer; it is an evidence-supported conclusion
- Root Cause can evolve across Sessions
- Root Cause is not the final output of a Case; Knowledge Assets are

---

### 3.9 Knowledge Assets

**Definition:** Reusable knowledge produced from completed Analysis Cases.

**Key properties:**

- Knowledge Assets belong to the Case, not individual Sessions
- They are the Case's final value output
- They represent the transformation from expertise to enterprise capability

**Examples:**

- SOP
- Pattern
- Rule
- Case
- Checklist
- Stage Definition
- Evidence Pattern
- Root Cause Pattern
- Expert Experience
- Workflow

---

## 4. Four-Type Classification

All domain objects in CEAP must belong to exactly one of four types:

| Type | Objective? | Role | Example |
|------|-----------|------|---------|
| **Evidence** | Yes | Fact | RTT=20ms, Log, Video, PCAP |
| **Observation** | No | Interpretation | RTT is normal, retransmission rate is slightly high |
| **Finding** | No | Conclusion | Network has slight packet loss |
| **Decision** | No | Action | Capture Server Log, close Case |

**This classification is mandatory.** Any object that cannot be classified into one of these four types requires re-evaluation.

---

## 5. Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-019 | Analysis Case is the platform-managed core object | Frozen |
| D-020 | Analysis Session belongs to Analysis Case | Frozen |
| D-021 | Knowledge Assets originate from Analysis Case | Frozen |
| D-022 | Root Cause is not the endpoint; Knowledge Asset is the final output | Frozen |
| D-023 | Analysis Session is an analysis activity, not a business object | Frozen |
| D-024 | Session's goal is reducing uncertainty, not necessarily finding Root Cause | Frozen |
| D-025 | Session success is creating analysis value, not ending analysis | Frozen |
| D-026 | Session is CEAP's smallest analysis recording unit | Frozen |
| D-027 | Investigation is an independent domain object | Frozen |
| D-028 | Session consumes Evidence but never produces Evidence | Frozen |
| D-029 | Four-Type Classification is mandatory for all domain objects | Frozen |
| D-030 | Investigation bridges Session output and new Evidence input | Frozen |

> **Note:** Decision IDs D-019 through D-030 are declared in this document and cross-referenced in other assets. No other document should redefine these IDs. See **WF-001 §5.2** for cross-asset consistency rules.

---

## Cross-References

- **ADR-001** — Analysis Case as core domain object
- **ADR-002** — Reasoning Framework operates within Sessions
- **ADR-003** — Evidence-driven analysis with traceability
- **B-001** — Investigation and Four-Type Classification
- **VF-001** — All concepts serve the Value Framework
- **FP-001** — This model implements the Core Transformation
- **CM-003** — Ubiquitous Language provides strict definitions
- **WF-001** — Asset production follows this workflow
