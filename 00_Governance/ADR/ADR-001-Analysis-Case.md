# ADR-001 Analysis Case as Core Domain Object

**Status:** Accepted
**Version:** v1.0
**Supersedes:** Original ADR-001 (Analysis Session as Core Domain Object)
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Context

Traditional communication problem analysis revolves around logs, videos, and tools.

This makes platform capabilities fragmented and difficult to evolve.

The platform requires a single stable domain object that can organize tools, workflows, AI, knowledge, and collaboration.

---

## Decision

### Analysis Case is the Core Domain Object

**Analysis Case** is defined as the core domain object of CEAP.

The platform manages Analysis Cases, not individual logs, parsers, or AI agents.

An Analysis Case represents:

> One complete business problem, from discovery to resolution and knowledge extraction.

An Analysis Case is the platform-managed object.
Not a single analysis activity.

### Analysis Case vs Analysis Session

| Aspect | Analysis Case | Analysis Session |
|--------|--------------|------------------|
| Nature | Business Object | Analysis Activity |
| Scope | One business problem | One analysis activity |
| Count | One per problem | Many per Case |
| Managed by platform | Yes (top-level) | No (belongs to Case) |
| Purpose | Track problem lifecycle | Reduce uncertainty |

```
Analysis Case
    ├── Analysis Session #1
    ├── Analysis Session #2
    ├── Analysis Session #3
    └── Analysis Session #N
```

Therefore:

- **Analysis Session** is an Activity.
- **Analysis Case** is a Business Object.

### Analysis Case Lifecycle

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

### Analysis Case Contents

```
Analysis Case
    ├── Metadata
    ├── Problem Description
    ├── Evidence
    ├── Investigation(s)
    ├── Analysis Session(s)
    ├── Observations
    ├── Findings
    ├── Hypotheses
    ├── Root Cause
    └── Knowledge Assets
```

**Note:** Knowledge Assets belong to the entire Analysis Case, not to any single Session. "Solution" has been removed — Root Cause and Knowledge Assets are the final outputs.

### Platform Responsibility

CEAP manages Analysis Cases, not individual reasoning activities.

The platform must support:

- Multi-expert collaboration
- Multiple analysis sessions
- Multiple investigation rounds
- Multiple verification versions
- Joint AI and expert participation

All of these occur within the same Analysis Case.

---

## Consequences

### Positive

1. **Platform centers on business problems**, not on tools or analysis activities.
2. **Multiple sessions can share the same Evidence.**
3. **Knowledge Assets are unified at the Case level.**
4. **Root Cause can evolve** across sessions — no requirement for first-session certainty.

### Negative / Risks

1. **Model complexity increases** — Case is a richer object than Session.
2. **Migration required** — existing designs centered on Session must be reoriented.

### Design Constraint

If the platform models around Session:

- Sessions cannot be organized
- Multiple analyses cannot be linked
- Knowledge cannot be uniformly accumulated

Therefore, the platform must model around **Analysis Case**.

---

## Architecture Decisions

> **Note:** Decision IDs D-019 through D-022 are canonically declared in **CM-002** (Core Concept Model). This table is retained for historical traceability. For authoritative declarations, see CM-002 §5.

| ID | Decision | Status |
|----|----------|--------|
| D-019 | Analysis Case is the platform-managed core object | Frozen |
| D-020 | Analysis Session belongs to Analysis Case | Frozen |
| D-021 | Knowledge Assets originate from Analysis Case | Frozen |
| D-022 | Root Cause is not the endpoint; Knowledge Asset is the final output | Frozen |

---

## Cross-References

- **CM-001** (deprecated) — Original concept model centered on Session
- **CM-002** — Updated concept model with Case as top-level object
- **CM-003** — Ubiquitous Language provides strict definitions of Case and Session
- **ADR-002** — Reasoning Framework operates within Sessions
- **ADR-003** — Evidence belongs to Case, consumed by Sessions
- **B-001** — Investigation and Four-Type Classification apply to Case
- **FP-001** — Case-level management implements the Core Transformation
- **WF-001** — This ADR follows the Architecture Decision Record guidelines
