# ADR-005 Agent Behavior Specification

**Status:** Accepted
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Context

From **AR-001**: Agent is the primary analysis executor, operating under Harness control. From **ADR-004**: Agent selects and composes Reasoning Models.

This document defines Agent's autonomous behavior, including Model selection, execution, confidence thresholds, and expert intervention triggers.

---

## Decision

### Agent Execution Lifecycle

```
Agent Start
    ↓
Analyze Problem Description + Evidence
    ↓
Select Reasoning Model(s) (auto-select, expert can override)
    ↓
Execute Reasoning Model(s)
    ↓
Produce Findings (with confidence)
    ↓
Check Confidence Thresholds
    ├── Above threshold → Continue autonomously
    └── Below threshold → Trigger expert intervention
    ↓
Produce Structured Output Document
    ↓
Expert Review (key checkpoints)
    ├── Accept → Continue
    ├── Correct → Agent re-reasons
    └── Manual Override → Expert takes over
    ↓
Agent learns from feedback (limited to current Case)
    ↓
Next Reasoning Model / Session End
```

### Reasoning Model Selection Strategy

**Agent auto-selection based on:**
1. Problem description keyword matching against Model registry
2. Evidence type analysis
3. Historical success rate of Models for similar problem types

**Selection process:**
```
Problem Description → Keyword Extraction → Model Registry Match
    ↓
Evidence Type → Capability Match → Model Candidate List
    ↓
Select Top-N Models → Execute in Priority Order
```

### Confidence Thresholds

| Threshold | Value | Trigger |
|-----------|-------|---------|
| Finding Confidence | ≥ 0.85 | Accept without expert review |
| Hypothesis Confidence | ≥ 0.70 | Continue tracking |
| Hypothesis Confidence | < 0.70 | Consider elimination |
| Investigation Request | Any | Expert review required |

### Expert Intervention Triggers

Expert is notified when:
1. Agent's Finding confidence < 0.85
2. Agent cannot eliminate Hypothesis after 3 iterations
3. Agent detects anomaly in reasoning chain
4. Expert proactively intervenes via Harness

### Model Orchestration Modes

| Mode | Description | Trigger |
|------|-------------|---------|
| **Sequential** | Execute Models one after another | Default mode |
| **Parallel** | Execute multiple Models concurrently | Complex problems, multi-team |
| **Conditional Branch** | Choose Model based on previous Model's output | Hypothesis-driven |

### Learning Context

Agent learns within current Case only:
- Tracks hypotheses tried and eliminated
- Records expert corrections
- Adjusts confidence thresholds based on feedback

---

## Consequences

1. Agent can autonomously execute most analysis without expert intervention.
2. Expert is notified at key decision points only.
3. Agent behavior is transparent and traceable.
4. Learning is contained within Case, preventing cross-contamination.

---

## Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-071 | Agent selects Reasoning Model via keyword + history matching | Frozen |
| D-072 | Finding confidence threshold: 0.85 | Frozen |
| D-073 | Hypothesis confidence threshold: 0.70 | Frozen |
| D-074 | Expert intervention triggered at 3 conditions | Frozen |
| D-075 | Agent supports Sequential, Parallel, Conditional Branch orchestration | Frozen |
| D-076 | Agent learning limited to current Case | Frozen |
| D-077 | Agent execution lifecycle follows 6-stage flow | Frozen |
| D-078 | Expert can override Model selection at any time | Frozen |
| D-079 | Agent produces Structured Output Document for expert review | Frozen |
| D-080 | Model orchestration default is Agent auto-select + expert override | Frozen |

---

## Cross-References

- **ADR-004** Reasoning Model Architecture — Agent selects and composes Models
- **AR-001** Architecture Design — Agent Harness design
- **DM-001** Domain Model — Agent LearningContext definition
- **CM-003** Ubiquitous Language — Agent, Harness, Confidence definitions
- **ADR-008** Structured Output Document — Agent output format
