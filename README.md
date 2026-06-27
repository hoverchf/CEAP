# Communication Experience Analysis Platform (CEAP)

CEAP is an Enterprise Communication Knowledge Platform.

Its goal is to continuously accumulate communication domain knowledge and transform expert experience into standardized methodologies, reusable knowledge assets, engineering capabilities, and AI-assisted analysis workflows.

The repository follows **Architecture-Driven Development** — all approved assets originate from Architecture Freeze and Deliverables.

---

## For New Contributors

Welcome to CEAP. This document will help you understand the repository structure and asset naming conventions.

### Repository Structure Overview

```
CEAP/
├── 00_Governance/          # Governance layer — strategy, principles, decisions
│   ├── Assets/             # Strategic assets (direction-setting)
│   ├── ADR/                # Architecture Decision Records (key choices)
│   ├── Decisions/          # Frozen decision index (reserved)
│   └── Workshop/           # Meeting records (process traceability)
│
├── 01_Knowledge/           # Knowledge layer — knowledge assets (Phase 3+)
├── 02_Engineering/         # Engineering layer — engineering assets (Phase 3+)
├── 03_Runtime/             # Runtime layer — runtime assets (Phase 3+)
│
├── docs/architecture/      # Design layer — design artifacts
│                           # Concept models, discoveries, workflows
│
├── README.md               # This file — asset index and contributor guide
├── ROADMAP.md              # Development roadmap and phase tracking
└── CHANGELOG.md            # Architecture milestone changelog
```

### Directory Definitions

| Directory | Full Name | Purpose |
|-----------|-----------|---------|
| `00_Governance/` | Governance | Strategic assets that define **why** we build and **what** principles guide us |
| `00_Governance/Assets/` | Governance Assets | High-level strategic documents: principles, value framework, definition, current state |
| `00_Governance/ADR/` | Architecture Decision Records | Documents recording key architectural choices and their rationale |
| `00_Governance/Decisions/` | Frozen Decisions Index | Central index of all frozen decisions (reserved for future use) |
| `00_Governance/Workshop/` | Workshop Records | Meeting notes from architecture discussions — process traceability |
| `01_Knowledge/` | Knowledge Layer | Reusable knowledge assets extracted from analysis (Phase 3+) |
| `02_Engineering/` | Engineering Layer | Engineering capabilities, SDKs, tools (Phase 3+) |
| `03_Runtime/` | Runtime Layer | Runtime execution assets, deployment configurations (Phase 3+) |
| `docs/architecture/` | Architecture Design Documents | Design-layer artifacts: concept models, discoveries, workflows |

### Asset Naming Conventions

| Prefix | Full Name | Description | Example |
|--------|-----------|-------------|---------|
| **AP** | Architecture Principles | Highest-level design rules governing all decisions | AP-001 |
| **ADR** | Architecture Decision Record | Documents a specific architectural choice | ADR-001 |
| **CM** | Concept Model | Defines domain objects and their relationships | CM-002 |
| **B** | Architecture Discovery | Significant insights that reshape the domain model | B-001 |
| **VF** | Value Framework | Defines how platform capabilities create enterprise value | VF-001 |
| **FP** | Freeze Point | Defines frozen platform boundaries and positioning | FP-001 |
| **BS** | Business State | Analyzes current enterprise state and identifies bottlenecks | BS-001 |
| **WF** | Workflow | Codifies working rules and processes | WF-001 |
| **PC** | Project Charter | Formal project authorization document (future) | PC-001 |
| **VS** | Vision Statement | Platform vision and aspirations (future) | VS-001 |
| **AR** | Architecture Document | Detailed architecture design (future) | AR-001 |
| **DM** | Domain Model | Implementation-level domain refinement (future) | DM-001 |

### Asset Status Definitions

| Status | Meaning | Can Change? |
|--------|---------|-------------|
| **Draft** | Under active discussion | Yes, freely |
| **Freeze Candidate** | Near-consensus, awaiting review | Minor changes only |
| **Frozen** | Formal baseline, consensus reached | Only via formal update process |
| **Deprecated** | Superseded by newer asset | No, read-only reference |

### How to Read an Asset Document

Every architecture asset follows a standard structure:

```markdown
# <Asset ID> <Title>

**Status:** Frozen
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## 1. Purpose / Context / Background
## 2. Decision / Definition / Model
## 3. Rationale / Principle
## 4. Consequences / Implications
## 5. Architecture Decisions (if applicable)
## 6. Cross-References
```

- **Purpose/Context** — Why does this asset exist?
- **Decision/Definition/Model** — What is the actual content?
- **Cross-References** — How does this relate to other assets?

### Governance vs Design: Two Layers

CEAP separates architecture work into two layers:

| Layer | Location | Answers | Contains |
|-------|----------|---------|----------|
| **Governance** | `00_Governance/` | Why? What? How do we decide? | Principles, decisions, value framework, definition, current state |
| **Design** | `docs/architecture/` | How do we model it? | Concept models, ubiquitous language, discoveries, workflows |

**Rule:** Governance assets define the rules. Design artifacts operate within those rules.

### Cross-Reference Format

Assets reference each other using the format:

```markdown
- **<Asset ID>** <Title> — relationship description
```

Example:

```markdown
- **ADR-001** — Analysis Case as core domain object
- **ADR-002** — Reasoning Framework operates within Sessions
```

This creates a navigable graph of all architecture decisions and their relationships.

---

## Architecture Assets

### Governance — Strategic Assets

Governance assets define the strategic direction, principles, and decisions.

| Asset | Description | Status |
|-------|-------------|--------|
| [AP-001](00_Governance/Assets/AP-001-Architecture-Principles.md) | Architecture Principles (13 principles) | Approved |
| [VF-001](00_Governance/Assets/VF-001-Value-Framework.md) | Value Framework — three-tier value hierarchy | Freeze Candidate |
| [FP-001](00_Governance/Assets/FP-001-CEAP-Definition.md) | CEAP Definition & Architecture Position | Frozen |
| [BS-001](00_Governance/Assets/BS-001-Current-State.md) | Current State Analysis — six core challenges | Freeze Candidate |

### Governance — Architecture Decisions

Architecture Decision Records document key architectural choices.

| Asset | Description | Status |
|-------|-------------|--------|
| [ADR-001](00_Governance/ADR/ADR-001-Analysis-Case.md) | Analysis Case as Core Domain Object | Accepted |
| [ADR-002](00_Governance/ADR/ADR-002-Reasoning-Framework.md) | Generic Reasoning Framework | Accepted |
| [ADR-003](00_Governance/ADR/ADR-003-Evidence-Driven-Analysis.md) | Evidence-Driven Analysis | Accepted |

### Design — Concept Models

Concept models define the structural and linguistic foundation of the architecture.

| Asset | Description | Status |
|-------|-------------|--------|
| [CM-001](docs/architecture/CM-001-Concept-Model-v0.1.md) | Concept Model v0.1 (deprecated) | Deprecated |
| [CM-002](docs/architecture/CM-002-Core-Concept-Model.md) | Core Concept Model — full domain model | Freeze Candidate |
| [CM-003](docs/architecture/CM-003-Ubiquitous-Language.md) | Ubiquitous Language — strict term definitions | Freeze Candidate |

### Design — Architecture Discoveries

Insights from architecture evolution that shaped the domain model.

| Asset | Description | Status |
|-------|-------------|--------|
| [B-001](docs/architecture/B-001-Investigation-and-Classification.md) | Investigation object & Four-Type Classification | Frozen |

### Design — Architecture Workflow

Working rules and processes for architecture governance.

| Asset | Description | Status |
|-------|-------------|--------|
| [WF-001](docs/architecture/WF-001-Architecture-Workflow.md) | Workshop process, asset production, self-review, governance, consistency checks | Freeze Candidate |

### Workshop Records

Process traceability records from architecture discussions.

| File | Content |
|------|---------|
| [00_Governance/Workshop/session-1.md](00_Governance/Workshop/session-1.md) | Value Framework discussion |
| [00_Governance/Workshop/session-2.md](00_Governance/Workshop/session-2.md) | CEAP Definition freeze |
| [00_Governance/Workshop/session-3.md](00_Governance/Workshop/session-3.md) | Architecture Principles |
| [00_Governance/Workshop/session-4.md](00_Governance/Workshop/session-4.md) | Current State analysis |
| [00_Governance/Workshop/session-5.md](00_Governance/Workshop/session-5.md) | Analysis Case concept |
| [00_Governance/Workshop/session-6.md](00_Governance/Workshop/session-6.md) | Analysis Session concept |
| [00_Governance/Workshop/session-7.md](00_Governance/Workshop/session-7.md) | Architecture refactoring |
| [00_Governance/Workshop/session-8.md](00_Governance/Workshop/session-8.md) | Investigation & Four-Type Classification |
| [00_Governance/Workshop/session-9.md](00_Governance/Workshop/session-9.md) | Reasoning model deep dive |
