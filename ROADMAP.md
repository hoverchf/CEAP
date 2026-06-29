# CEAP Roadmap

## Current Version

Bootstrap v0.4 — Phase 3 Complete, Phase 4 Starting

---

## Completed

### Phase 1: Foundation (M001 - M002)

| Asset | Description | Status |
|-------|-------------|--------|
| AP-001 | Architecture Principles (13 principles) | Approved |
| FP-001 | CEAP Definition & Architecture Position | Frozen |
| VF-001 | Value Framework — three-tier value hierarchy | Frozen |
| BS-001 | Current State Analysis — six core challenges | Frozen |

### Phase 2: Domain Model (M003)

| Asset | Description | Status |
|-------|-------------|--------|
| CM-001 | Concept Model v0.1 (deprecated) | Deprecated |
| CM-002 | Core Concept Model — full domain model (v1.2) | Frozen |
| CM-003 | Ubiquitous Language — strict term definitions (v1.2) | Frozen |
| B-001 | Investigation object & Four-Type Classification | Frozen |
| ADR-001 | Analysis Case as Core Domain Object | Accepted |
| ADR-002 | Generic Reasoning Framework | Accepted |
| ADR-003 | Evidence-Driven Analysis | Accepted |
| WF-001 | Architecture Workflow (v1.1) | Frozen |
| WF-002 | Architecture Working Norms — chief architect standards | Frozen |

### Phase 3: Architecture Design (M004)

| Asset | Description | Status |
|-------|-------------|--------|
| VS-001 | Vision Statement | Frozen |
| PC-001 | Project Charter — scope, milestones, organization | Frozen |
| AR-001 | Architecture Design — four-layer system architecture (v0.3) | Frozen |
| DM-001 | Domain Model — implementation-level refinement (v0.5) | Frozen |

---

### Phase 4: Engineering Design (M006 - M008)

| Asset | Description | Status |
|-------|-------------|--------|
| ADR-004 | Reasoning Model Architecture — 8 models, interface, composition | Accepted |
| ADR-005 | Agent Behavior Specification — execution lifecycle, confidence thresholds | Accepted |
| ADR-006 | Data Layer Specification — collector, upload, storage, download, adapters | Accepted |
| ADR-007 | Knowledge Asset Schema — 9 asset types with schemas | Accepted |
| ADR-008 | Structured Output Document — 10-section analysis report | Accepted |
| ADR-009 | Multi-Team Collaboration — parallel/serial orchestration | Accepted |

---

## In Progress

| Priority | Work Item | Description | Depends On |
|----------|-----------|-------------|------------|
| **P2** | **CM-003 Updates** | Add Validation, Solution (if needed) to ubiquitous language | CM-003 v1.2 |

---

## Upcoming

### Phase 4: Engineering

| Priority | Work Item | Description | Depends On |
|----------|-----------|-------------|------------|
| P1 | 01_Knowledge Layer | Knowledge asset storage, versioning, search | Knowledge Asset Schema |
| P1 | 02_Engineering Layer | Platform adapters, log parsers, data pipeline | Data Layer Specification |
| P1 | 03_Runtime Layer | Agent Harness runtime, Agent execution engine | Agent Behavior Specification |
| P2 | Multi-Team Collaboration | Team session isolation, output passing | DM-001 §15 |
| P2 | Problem Family Management | Family analysis methodology evolution, shared knowledge assets | DM-001 §2 |

### Phase 5: AI & Reasoning

| Priority | Work Item | Description | Depends On |
|----------|-----------|-------------|------------|
| P1 | Reasoning Model Implementation | Recursive Narrowing, Timeline Reconstruction, Protocol State Machine | Reasoning Model Design |
| P1 | Agent Harness Implementation | Direction control, behavior tuning, result validation, manual override | Agent Behavior Specification |
| P2 | Agent Learning | Case-level learning, hypothesis elimination tracking, expert correction history | Agent Behavior Specification |
| P2 | Knowledge Asset Auto-Extraction | Agent automatically extracts knowledge assets from completed Cases | Knowledge Asset Schema |

### Phase 6: Platform Capability

| Priority | Work Item | Description | Depends On |
|----------|-----------|-------------|------------|
| P2 | Case Search & Analytics | Search cases by Problem Family, Evidence type, Root Cause pattern | Data Layer Specification |
| P2 | Team Analytics Dashboard | Efficiency metrics, quality metrics, knowledge asset growth | Multi-Team Collaboration |
| P2 | Non-Communication Domain Extension | Extend platform to non-communication analysis domains | All above |

---

## Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-059 | Roadmap reorganized into 6 phases with priority levels | Frozen |
| D-060 | P0 items (Reasoning Model, Agent Behavior) are the next immediate focus | Frozen |
| D-061 | Phase 4 Engineering starts only after P0 items are designed | Frozen |

---

## Cross-References

- **VS-001** Vision Statement — Roadmap aligns with vision
- **VF-001** Value Framework — Roadmap follows value evolution
- **PC-001** Project Charter — Roadmap extends charter milestones
- **WF-001** Architecture Workflow — Roadmap follows workflow rules
- **WF-002** Architecture Working Norms — Roadmap managed per norms
