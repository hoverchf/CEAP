# WF-001 Architecture Workflow

**Status:** Freeze Candidate
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Purpose

This document codifies the working rules and processes extracted from all CEAP architecture discussions, assets, and design practices.

It answers: **How do we do architecture at CEAP?**

---

## 1. Workshop Discussion Workflow

### 1.1 Structure

Each Workshop session follows this pattern:

```
Discussion
    ↓
Consensus Formation
    ↓
Self-Review (Architect主动修正)
    ↓
Asset Identification (是否需要产出正式资产)
    ↓
Decision Classification (Freeze / Freeze Candidate / 暂不 Freeze)
```

### 1.2 Rules

- **Discussion produces consensus, not just notes.** Every session must end with explicit decisions.
- **Self-review is mandatory.** The architect must proactively identify and correct their own prior mistakes or inconsistencies. This is not optional — it is a core discipline.
- **Not every discovery should be frozen immediately.** Some findings (classified as B-type discoveries) affect multiple assets and must wait for a broader review before freezing.

### 1.3 Session Numbering

Workshop sessions are numbered sequentially (`session-N.md`) in `workshop-summary/`.

They serve as **traceability records**, not formal architecture assets.

---

## 2. Architecture Asset Production

### 2.1 Asset Types

| Type | Location | Convention |
|------|----------|------------|
| Governance Assets | `00_Governance/Assets/` | AP-xxx, VF-xxx, FP-xxx, BS-xxx |
| Architecture Decisions | `00_Governance/ADR/` | ADR-xxx |
| Concept Models | `docs/architecture/` | CM-xxx |
| Architecture Discoveries | `docs/architecture/` | B-xxx |
| Architecture Workflow | `docs/architecture/` | WF-xxx |

### 2.2 Naming Convention

```
<category>-<seq> - <title>
```

Categories:

| Prefix | Category | Example |
|--------|----------|---------|
| AP | Architecture Principles | AP-001 |
| ADR | Architecture Decision Record | ADR-001 |
| CM | Concept Model | CM-001 |
| B | Architecture Discovery (B-type, not yet fully stable) | B-001 |
| VF | Value Framework | VF-001 |
| FP | Freeze Point | FP-001 |
| BS | Business State / Current State | BS-001 |
| PC | Project Charter | PC-001 |
| VS | Vision Statement | VS-001 |
| AR | Architecture Document | AR-001 |
| DM | Domain Model | DM-001 |

### 2.3 Asset Structure

Every architecture asset MUST follow this structure:

```markdown
# <Asset ID> <Asset Title>

**Status:** <Approved | Accepted | Freeze Candidate | Frozen | Deprecated>
**Version:** <semver or vN.N>
**Created:** <YYYY-MM-DD>
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## 1. Purpose / Context / Background

## 2. Decision / Definition / Model

## 3. Rationale / Principle

## 4. Consequences / Implications

## 5. Architecture Decisions (if applicable)

| ID | Decision | Status |

---

## 6. Cross-References

- **AP-001** — Architecture Principles define the governance rules this workflow enforces
- **FP-001** — CEAP Definition sets the platform position this workflow serves
- **VF-001** — Value Framework defines the value evolution this workflow supports
- **BS-001** — Current State Analysis provides the context this workflow addresses
- **CM-002** — Core Concept Model is the structural output of this workflow
- **CM-003** — Ubiquitous Language is the terminology standard this workflow maintains
- **B-001** — Investigation & Classification is a discovery produced by this workflow
- **ADR-001** — Analysis Case decision is governed by this workflow
- **ADR-002** — Reasoning Framework decision is governed by this workflow
- **ADR-003** — Evidence-Driven Analysis decision is governed by this workflow
- **ROADMAP** — This workflow follows the value-driven sequencing defined in VF-001

### 2.4 Mandatory Sections

- **Purpose/Context** — Why does this asset exist?
- **Decision/Definition/Model** — What is the actual content?
- **Cross-References** — How does this relate to other assets?

### 2.5 Optional Sections

- **Rationale** — Why this decision over alternatives?
- **Consequences** — Positive and negative outcomes.
- **Negative / Risks** — What could go wrong?

---

## 3. Self-Review Discipline

### 3.1 What It Is

Self-review is the architect's proactive identification and correction of their own prior mistakes, inconsistencies, or incomplete thinking.

### 3.2 When It Happens

Self-review occurs at the end of every Workshop session.

### 3.3 What to Look For

| Check | Example |
|-------|---------|
| Terminology drift | "Knowledge" → "Knowledge Assets" |
| Structural inconsistency | Evidence belonging to Session instead of Case |
| Over-abstraction | Too many principles (13 → 7) |
| Missing concepts | Hypothesis was absent from the model |
| False equivalences | Treating Observation and Finding as the same thing |
| Premature freezing | B-type discoveries frozen before full impact assessment |

### 3.4 Self-Review Output

The architect documents:

1. **What was wrong/incomplete** — the prior state
2. **What the correction is** — the new state
3. **Why it matters** — the architectural impact
4. **What else needs updating** — cross-reference cleanup

### 3.5 Discovery Classification

During self-review, discoveries are classified:

| Class | Meaning | Action |
|-------|---------|--------|
| **A** | Stable, low-impact change | Freeze immediately |
| **B** | Significant, affects multiple assets | Defer freeze until broader review |

---

## 4. Asset Governance Workflow

### 4.1 Status Lifecycle

```
Draft
    ↓
Freeze Candidate (under discussion, may change)
    ↓
Frozen (consensus reached, stable baseline)
    ↓
Deprecated (superseded by newer asset)
```

### 4.2 Status Definitions

| Status | Meaning | Can Change? |
|--------|---------|-------------|
| **Draft** | Under active discussion | Yes, freely |
| **Freeze Candidate** | Near-consensus, awaiting review | Minor changes only |
| **Frozen** | Formal baseline | Only via formal update process |
| **Deprecated** | Superseded by newer asset | No, read-only reference |

### 4.3 Freeze Criteria

An asset is eligible for freezing when:

1. All explicit decisions have been recorded with IDs
2. Cross-references to/from other assets are complete
3. Self-review has been performed and documented
4. The reviewer (Project Owner) has acknowledged

### 4.4 Update Process

When a frozen asset needs updating:

1. Identify the impact scope (which other assets are affected?)
2. Classify the change (A-type = minor, B-type = significant)
3. For B-type: defer to the next relevant Workshop session
4. Update the asset, mark the old version as Deprecated
5. Update all cross-references
6. Update CHANGELOG.md

---

## 5. Cross-Asset Consistency Checks

### 5.1 Dependency Graph

Every asset must declare its relationships. Before modifying any asset, check:

```
FP-001 (CEAP Definition)
    ↑ governs
AP-001 (Architecture Principles)
    ↑ informs
VF-001 (Value Framework) ←→ BS-001 (Current State)
    ↑ realized by
CM-002 (Core Concept Model) ←→ CM-003 (Ubiquitous Language)
    ↑ enforced by
ADR-001 (Analysis Case) ←→ ADR-002 (Reasoning) ←→ ADR-003 (Evidence)
    ↑ shaped by
B-001 (Investigation & Classification)
```

### 5.2 Consistency Rules

| Rule | Check |
|------|-------|
| **Terminology** | All assets use the same terms as CM-003 |
| **Value mapping** | All capabilities map to VF-001 |
| **Positioning** | No asset contradicts FP-001 |
| **Principles** | No asset violates AP-001 |
| **Cross-ref integrity** | Every `**Asset-ID**` reference resolves to an existing file |
| **Decision ID uniqueness** | No duplicate D-xxx IDs across assets |

### 5.3 Cross-Reference Maintenance

Every asset MUST include a Cross-References section listing:

- Which assets it depends on
- Which assets depend on it
- How it relates to each

---

## 6. Architecture Decision Record (ADR) Guidelines

### 6.1 When to Create an ADR

Create an ADR when:

1. A significant architectural choice is made
2. A shift in architectural direction occurs
3. A new architectural pattern is adopted
4. An existing design is proven insufficient

### 6.2 ADR Structure

```markdown
# ADR-xxx <Title>

**Status:** Accepted
**Version:** v1.0
**Created:** <YYYY-MM-DD>
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Context
Why are we making this decision?

## Decision
What did we decide?

## Principle
What guiding rule does this establish?

## Consequences
What changes? What breaks?
```

### 6.3 ADR Naming

- ADR-001: Core object shift (Session → Case)
- ADR-002: Framework design (Reasoning Framework)
- ADR-003: Analysis methodology (Evidence-Driven)

---

## 7. Roadmap Alignment

### 7.1 Value-Driven Sequencing

The roadmap follows the Value Evolution order from VF-001:

```
Phase 1: Foundation
    - AP-001 (Principles) ✓
    - FP-001 (Definition) ✓
    - VF-001 (Value Framework) ✓
    - BS-001 (Current State) ✓

Phase 2: Domain Model
    - CM-001 → CM-002 (Core Concepts) ✓
    - CM-003 (Ubiquitous Language) ✓
    - B-001 (Investigation & Classification) ✓
    - ADR-001, 002, 003 ✓

Phase 3: Detailed Architecture
    - PC-001 (Project Charter)
    - VS-001 (Vision)
    - AR-001 (Architecture)
    - DM-001 (Domain Model)

Phase 4: Reasoning Deep-Dive
    - Reasoning Model specification
    - AI Agent design
```

### 7.2 Phase Gate

Each phase completes only when:

1. All assets in that phase are Frozen
2. Cross-references are consistent
3. CHANGELOG.md is updated
4. ROADMAP.md reflects current status

---

## 8. Repository Structure Rules

### 8.1 Directory Convention

```
CEAP/
├── 00_Governance/          # Governance layer
│   ├── Assets/             # Strategic assets (AP, VF, FP, BS)
│   ├── ADR/                # Architecture Decision Records
│   ├── Decisions/          # Frozen decision index
│   └── Workshop/           # Meeting records
├── 01_Knowledge/           # Reserved for knowledge assets
├── 02_Engineering/         # Reserved for engineering assets
├── 03_Runtime/             # Reserved for runtime assets
├── docs/
│   └── architecture/       # ADR, CM, B-type assets
├── README.md
├── ROADMAP.md
└── CHANGELOG.md
```

### 8.2 Rule

Never store architecture assets in directories that imply implementation (01_Knowledge, 02_Engineering, 03_Runtime) until those phases are active.

---

## 9. Quick Reference Checklist

### Before Starting a Workshop Session

- [ ] Review existing assets for context
- [ ] Identify which frozen assets might be impacted
- [ ] Prepare draft asset structure

### After Each Workshop Session

- [ ] Document all decisions with IDs
- [ ] Perform self-review (look for corrections needed)
- [ ] Classify discoveries (A-type or B-type)
- [ ] Determine freeze status for each asset
- [ ] Update cross-references in related assets

### Before Freezing an Asset

- [ ] All decisions have unique IDs
- [ ] Cross-references are complete
- [ ] Self-review is documented
- [ ] Project Owner has reviewed

### Before Updating a Frozen Asset

- [ ] Impact scope assessed (which other assets affected?)
- [ ] Change classified (A-type or B-type)
- [ ] Cross-references updated
- [ ] CHANGELOG.md updated
- [ ] Old version marked appropriately (Deprecated / superseded)
