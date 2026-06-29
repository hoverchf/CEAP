# ADR-004 Reasoning Model Architecture

**Status:** Accepted
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Context

From **ADR-002**: "Reasoning Model is CEAP's differentiator. Reasoning Models are pluggable strategies, not platform architecture."

A Case can use multiple Reasoning Models in combination. Agent needs to select, compose, and execute them. Expert can override Agent's selection via Harness.

---

## Decision

### CEAP Defines 8 Reasoning Models

| # | Reasoning Model | Description | Typical Scenario |
|---|----------------|-------------|-----------------|
| 1 | **Recursive Narrowing** | Gradually narrow problem space based on evidence | Almost all problems — narrow scope to a specific module or node |
| 2 | **Timeline Reconstruction** | Reconstruct event timeline across modules to determine dependencies | Multi-module event analysis — determine if event A happened before/after event B |
| 3 | **Rule Matching** | Match evidence against known rules; violation = anomaly | Known protocol behaviors, counter anomalies |
| 4 | **Decision Tree** | Step-by-step fault tree localization | Common fault diagnosis — follow symptoms to root module |
| 5 | **Protocol State Machine** | Restore protocol state from evidence, identify abnormal transitions | Standard protocols — VoLTE, SIP, 5G signaling |
| 6 | **Pattern Matching** | Match evidence pattern to known root cause patterns | Known patterns from previous cases |
| 7 | **LLM Guided Reasoning** | Use LLM for open-ended reasoning without explicit rules | Unknown protocols, text-based reasoning |
| 8 | **Multi-Model Ensemble** | Run multiple models in parallel, compare results | Complex problems requiring multiple perspectives |

### Reasoning Model Interface

```
ReasoningModel
    ├── name: String
    ├── description: String
    ├── input: List<Evidence + Observation + Hypothesis>
    ├── output: List<Finding + InvestigationRequest>
    ├── confidence: Float (0.0 - 1.0)
    ├── reasoning_chain: List<Step>
    └── status: Enum (Running / Completed / Terminated)

Step
    ├── step_id: UUID
    ├── type: Enum (OBSERVATION / HYPOTHESIS / FINDING / DECISION)
    ├── content: String
    ├── supporting_evidence: List<UUID>
    ├── confidence: Float
    └── timestamp: DateTime
```

### Model Composition

Multiple Reasoning Models can be composed within a single Case:

```
Case
    ↓
Recursive Narrowing → Finding: "AP layer anomaly"
    ↓
Timeline Reconstruction → Finding: "Event X before Event Y"
    ↓
Protocol State Machine → Finding: "RRC state transition abnormal"
    ↓
Pattern Matching → Root Cause: "Similar to Case #42"
```

### Model Selection

- **Agent default:** Agent automatically selects Reasoning Model based on problem description and evidence type
- **Expert override:** Expert can specify Model via Harness Direction Setter
- **Model registry:** Each Model registers name, description, applicable scenarios

### Data Sharing Between Models

All Model outputs (Finding, InvestigationRequest) are written to Case shared space. Next Model reads from Case.

```
Model A → Finding → Case Shared Space
    ↓
Model B ← reads Finding ← Case Shared Space
    ↓
Model B → Investigation Request → Real World → New Evidence → Case
    ↓
Model C ← reads Finding + New Evidence ← Case Shared Space
```

---

## Consequences

1. Agent can compose Reasoning Models flexibly within a Case.
2. Expert can override Agent's Model selection at any time.
3. All Model outputs are traceable via reasoning_chain.
4. New Reasoning Models can be added to the registry without architecture changes.

---

## Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-062 | CEAP defines 8 standard Reasoning Models | Frozen |
| D-063 | Reasoning Models use a unified interface | Frozen |
| D-064 | Multiple Models can be composed within a Case | Frozen |
| D-065 | Model data is shared via Case shared space | Frozen |
| D-066 | Agent auto-selects Model, expert can override | Frozen |
| D-067 | Model registry enables extensibility | Frozen |
| D-068 | Each Model output includes reasoning_chain for traceability | Frozen |
| D-069 | New domain problems should only require new Reasoning Models | Frozen |
| D-070 | Reasoning Model is CEAP's highest-leverage design activity | Frozen |

---

## Cross-References

- **ADR-002** Reasoning Framework — Reasoning Model is a pluggable strategy
- **ADR-005** Agent Behavior Specification — Agent orchestrates Reasoning Models
- **AR-001** Architecture Design — Reasoning Model belongs to Capability Layer
- **DM-001** Domain Model — Model outputs stored in Case shared space
- **CM-003** Ubiquitous Language — Reasoning Model, Finding, Evidence, Hypothesis definitions
