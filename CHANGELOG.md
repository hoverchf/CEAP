## M002: Architecture Foundation

### Added

- VF-001 Value Framework
- FP-001 CEAP Definition & Architecture Position
- BS-001 Current State Analysis
- CM-001 Concept Model v0.1 (deprecated, replaced by CM-002)
- CM-002 Core Concept Model (replaces CM-001)
- CM-003 Ubiquitous Language
- B-001 Investigation & Four-Type Classification
- ADR-001 Analysis Case as Core Domain Object
- ADR-002 Reasoning Framework
- ADR-003 Evidence-Driven Analysis
- WF-001 Architecture Workflow

### Architecture Status

Architecture Foundation Established

---

## M003: Architecture Baseline

### Added

- VS-001 Vision Statement
- PC-001 Project Charter
- AR-001 Architecture Design (four-layer system architecture)
- DM-001 Domain Model (implementation-level refinement)
- Workshop records: session-10, session-11, session-12

### Updated

- AP-001: Principle 8 Evidence/Observation order corrected (v1.1)
- CM-002: Added Problem Family, fixed section numbering, updated lifecycle (v1.2)
- CM-003: Added Problem Family, Agent, Harness, Team definitions (v1.2)
- DM-001: v0.1 → v0.5 (Session restored, Problem Type → Problem Family, team collaboration revised, cross-refs updated)
- AR-001: v0.1 → v0.3 (removed Analysis Engine, Agent is sole analyzer, Harness philosophy clarified, cross-refs updated)
- B-001: Fixed section heading (B-002 → B-001)
- WF-001: Added Approved/Accepted to status definitions (v1.1)
- ADR-001: Removed "Solution" from Case Contents
- VF-001: Clarified Knowledge vs Knowledge Assets distinction
- README.md: Full asset inventory with new contributor guide, removed duplicate entries
- ROADMAP.md: Updated with all completed assets
- CHANGELOG.md: Restructured with M002/M003/M004 milestones
- WF-002: New — Chief Architect working norms

### Asset Status Updates

- AP-001: v1.0 → v1.1
- CM-002: v1.0 → v1.2
- CM-003: v1.0 → v1.2
- DM-001: v0.1 → v0.5
- AR-001: v0.1 → v0.3
- WF-001: v1.0 → v1.1
- WF-002: New (v1.0)

### Architecture Status

Architecture Foundation Established — Core Concepts Frozen
Phase 3 (Vision, Charter, Architecture, Domain Model) Completed

## M005: Roadmap Reorganization

### Updated

- ROADMAP.md: Reorganized into 6 phases with priority levels (P0/P1/P2)
- ROADMAP.md: v0.4 → v1.0

### Architecture Decisions

- D-059: Roadmap reorganized into 6 phases with priority levels
- D-060: P0 items (Reasoning Model, Agent Behavior) are the next immediate focus
- D-061: Phase 4 Engineering starts only after P0 items are designed

## M006: Reasoning & Agent Design

### Added

- ADR-004 Reasoning Model Architecture (8 models, interface, composition, selection)
- ADR-005 Agent Behavior Specification (execution lifecycle, confidence thresholds, orchestration)

### Architecture Decisions

- D-062 ~ D-070: Reasoning Model decisions
- D-071 ~ D-080: Agent Behavior decisions

## M007: Data & Knowledge & Output

### Added

- ADR-006 Data Layer Specification (collector, upload, storage, download, adapters)
- ADR-007 Knowledge Asset Schema (9 asset types with schemas)
- ADR-008 Structured Output Document (10-section analysis report)
- ADR-009 Multi-Team Collaboration (parallel/serial orchestration)

### Architecture Decisions

- D-081 ~ D-090: Data Layer decisions
- D-091 ~ D-099: Knowledge Asset decisions
- D-100 ~ D-104: Structured Output Document decisions
- D-105 ~ D-114: Multi-Team Collaboration decisions

### Architecture Status

Phase 4 Engineering Design Complete — All ADRs Accepted
