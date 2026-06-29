# ADR-008 Structured Output Document

**Status:** Accepted
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Context

From **AR-001 §2.2**: Agent outputs a structured analysis document. Expert validates Agent's reasoning by reviewing the Evidence → Observation → Finding chain.

This document must be both human-readable (for expert review) and structured (for future machine processing). Current phase prioritizes human readability.

---

## Decision

### Document Structure (10 Sections)

```
Analysis Report
    ├── §1. Case Summary
    ├── §2. Evidence Summary
    ├── §3. Observations
    ├── §4. Hypotheses
    │       ├── Active Hypotheses
    │       └── Eliminated Hypotheses
    ├── §5. Findings
    │       └── Supporting Evidence Chain
    ├── §6. Root Cause
    ├── §7. Investigation Requests
    ├── §8. Reasoning Trace
    ├── §9. Expert Review Summary
    └── §10. Knowledge Asset Candidates
```

### Section Details

#### §1. Case Summary

| Field | Description |
|-------|-------------|
| `case_id` | Case unique identifier |
| `problem_family` | Problem Family name |
| `problem_description` | Original problem description |
| `analysis_date` | When analysis was performed |
| `agent_name` | Agent that performed analysis |

#### §2. Evidence Summary

Evidence grouped by type with key statistics:

| Field | Description |
|-------|-------------|
| `evidence_type` | AP_LOG / MODEM_LOG / NET_LOG / VIDEO / ... |
| `file_count` | Number of files |
| `total_size` | Total data size |
| `time_range` | Time range covered |
| `annotated_areas` | Test team annotations |

#### §3. Observations

| Field | Description |
|-------|-------------|
| `observation_id` | Unique identifier |
| `content` | Observation content |
| `evidence_refs` | Supporting Evidence references |
| `generated_by` | AGENT / EXPERT / MANUAL_OVERRIDE |
| `confidence` | 0.0 - 1.0 |
| `timestamp` | When observed |

#### §4. Hypotheses

**Active Hypotheses:**
| Field | Description |
|-------|-------------|
| `hypothesis_id` | Unique identifier |
| `content` | Hypothesis content |
| `supporting_observations` | Supporting Observation references |
| `confidence` | 0.0 - 1.0 |
| `status` | ACTIVE |

**Eliminated Hypotheses:**
| Field | Description |
|-------|-------------|
| `hypothesis_id` | Unique identifier |
| `content` | Hypothesis content |
| `elimination_reason` | Why eliminated |
| `elimination_evidence` | Evidence that disproved it |
| `status` | ELIMINATED |

#### §5. Findings

| Field | Description |
|-------|-------------|
| `finding_id` | Unique identifier |
| `content` | Finding content |
| `evidence_chain` | Complete chain: Evidence → Observation → Hypothesis → Finding |
| `confidence` | 0.0 - 1.0 |
| `generated_by` | AGENT / EXPERT / MANUAL_OVERRIDE |

**Evidence Chain Visualization:**
```
Finding: Network has minor packet loss (confidence=0.85)
    └── Hypothesis: WiFi AP anomaly (confidence=0.80)
        └── Observation: Retransmission rate slightly elevated (confidence=0.95)
            └── Evidence: TCP Retransmission = 3% (confidence=1.0)
```

#### §6. Root Cause

| Field | Description |
|-------|-------------|
| `root_cause` | Root cause description |
| `supporting_findings` | Supporting Finding references |
| `evidence_chain_summary` | Summary of complete evidence chain |
| `confidence` | 0.0 - 1.0 |
| `confirmed_by` | Confirming expert (initially empty) |

#### §7. Investigation Requests

| Field | Description |
|-------|-------------|
| `request_id` | Unique identifier |
| `request` | What to investigate |
| `target` | Investigation target |
| `assigned_team` | Responsible team |
| `status` | Pending / In Progress / Completed |

#### §8. Reasoning Trace

| Field | Description |
|-------|-------------|
| `step_id` | Unique identifier |
| `step_order` | Sequence number |
| `reasoning_model` | Model used for this step |
| `action` | What Agent did |
| `reasoning` | Why Agent did it |
| `confidence` | Step confidence |
| `timestamp` | When step executed |

#### §9. Expert Review Summary

| Field | Description |
|-------|-------------|
| `review_status` | Pending / Accepted / Corrected / Rejected |
| `corrections` | Expert corrections applied |
| `manual_overrides` | Expert manual interventions |
| `review_timestamp` | When reviewed |
| `reviewed_by` | Reviewing expert |

#### §10. Knowledge Asset Candidates

| Field | Description |
|-------|-------------|
| `candidate_id` | Unique identifier |
| `asset_type` | SOP / WORKFLOW / SKILL / EVIDENCE_PATTERN / ROOT_CAUSE_PATTERN |
| `content_summary` | What should be extracted |
| `auto_extracted` | Whether Agent auto-identified this |
| `confirmation_required` | Expert confirmation needed |

---

## Document Lifecycle

```
Agent produces draft → Expert reviews → Expert accepts/corrects
    ↓
Agent re-reasons (if corrected) → Updated draft
    ↓
Expert confirms final version
    ↓
Document archived with Case
    ↓
Knowledge Asset Candidates → extracted by Asset Extractor
```

---

## Consequences

1. Expert can efficiently validate Agent's analysis by reviewing structured evidence chain.
2. All reasoning is traceable via §8 Reasoning Trace.
3. Expert corrections are recorded in §9 Expert Review Summary.
4. Knowledge Asset Candidates are auto-identified for extraction.
5. Current phase: human-readable Markdown; future: machine-processable structured format.

---

## Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-100 | Structured Output Document has 10 standard sections | Frozen |
| D-101 | Evidence chain visualization shows complete reasoning path | Frozen |
| D-102 | Expert review results are recorded in §9 | Frozen |
| D-103 | Knowledge Asset Candidates are auto-identified by Agent | Frozen |
| D-104 | Current phase: human-readable format; future: structured format | Frozen |

---

## Cross-References

- **AR-001** Architecture Design — §2.2 Structured Output Document
- **DM-001** Domain Model — Root Cause Evidence Chain (DM-001 §5)
- **CM-003** Ubiquitous Language — Evidence, Observation, Hypothesis, Finding, Root Cause definitions
- **ADR-004** Reasoning Model Architecture — Reasoning Trace structure
- **ADR-005** Agent Behavior Specification — Agent produces this document
- **ADR-007** Knowledge Asset Schema — §10 Knowledge Asset Candidates
