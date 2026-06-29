# WF-002 Chief Architect Working Norms

**Status:** Frozen
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Purpose

This document codifies the working norms for the Chief Architect role in CEAP.

These norms are derived from lessons learned during the M003 baseline maintenance process.

They apply to every architectural decision, document change, and asset submission.

---

## 1. Pre-Change Checklist

Before making any change to any architecture asset, the Chief Architect MUST:

- [ ] Review CM-003 (Ubiquitous Language) for term consistency
- [ ] Review AP-001 (Architecture Principles) for principle compliance
- [ ] Review FP-001 (CEAP Definition) for positioning alignment
- [ ] Review VF-001 (Value Framework) for value mapping
- [ ] Review BS-001 (Current State) for challenge coverage
- [ ] Identify impact scope (which other assets are affected?)
- [ ] Classify the change (A-type = minor, B-type = significant)
- [ ] For B-type: defer to the next relevant Workshop session

---

## 2. Term Introduction Protocol

When introducing a new term to the architecture:

1. **First:** Update CM-003 (Ubiquitous Language) with the new term definition
2. **Then:** Update all other documents that use the new term
3. **Finally:** Update CM-002 (Core Concept Model) if the term is a domain concept

**Rule:** No document may introduce a new term without first updating CM-003.

---

## 3. Impact Assessment Protocol

When a change may affect frozen assets:

1. **Identify:** List all documents that reference the affected concept
2. **Assess:** Classify the change (A-type or B-type per WF-001 §3.5)
3. **Plan:** For B-type, plan a broader review before freezing
4. **Execute:** Update ALL affected documents (not just the one being edited)
5. **Verify:** Use full-text search (grep) to confirm no stale references remain

**Rule:** Never assume a change only affects one document. Always verify with grep.

---

## 4. Self-Review Discipline

Before submitting any asset for Project Owner review, the Chief Architect MUST perform self-review:

### 4.1 Terminology Check

- Every term matches CM-003 definition
- No bare "Knowledge" where "Knowledge Assets" is required
- No "Evidence Collection" where "Investigation" is the defined term
- No undefined terms (Agent, Harness, Team, Problem Family, etc.)

### 4.2 Structural Check

- Metadata header is complete (Status, Version, Created, Owner, Reviewer)
- Section numbering is sequential
- Tables are properly formatted
- Cross-references section exists and is complete

### 4.3 Consistency Check

- No contradiction with FP-001 (platform positioning)
- No violation of AP-001 (architecture principles)
- No conflict with CM-002 (concept model)
- No duplicate Decision IDs
- No stale references to removed concepts

### 4.4 Version Control

- Version number incremented on change
- CHANGELOG.md updated with change description
- ROADMAP.md updated if milestone status changes
- Previous version marked as Deprecated if superseded

---

## 5. Architectural Challenge Protocol

The Chief Architect has a responsibility to challenge decisions, not merely accept them.

### When to Challenge

- A proposed change contradicts FP-001 (platform positioning)
- A proposed change violates AP-001 (architecture principles)
- A proposed change introduces unnecessary complexity
- A proposed change conflicts with established domain model
- A proposed change lacks sufficient justification

### How to Challenge

1. Present the architectural concern with specific references
2. Propose alternative solutions
3. Explain the long-term impact of the proposed change
4. Escalate to Project Owner if disagreement persists

**Rule:** The Project Owner has final authority, but the Chief Architect must present professional dissent when warranted.

---

## 6. Documentation Standards

### 6.1 Asset Structure

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
## 6. Cross-References
```

### 6.2 Cross-Reference Format

Every asset MUST include a Cross-References section listing:

- Which assets it depends on
- Which assets depend on it
- How it relates to each

Format: `- **<Asset ID>** — relationship description`

### 6.3 Decision ID Rules

- Each Decision ID (D-xxx) is declared in exactly ONE canonical document
- Other documents may reference the same decision but must note the canonical source
- Decision IDs must be contiguous within each asset
- No duplicate Decision IDs across the repository

---

## 7. Change Management

### 7.1 Status Transitions

```
Draft
    ↓ (self-review passed, submitted to Project Owner)
Freeze Candidate
    ↓ (Project Owner approved)
Frozen
    ↓ (superseded by newer asset)
Deprecated
```

### 7.2 Update Process for Frozen Assets

1. Identify impact scope (which other assets are affected?)
2. Classify the change (A-type = minor, B-type = significant)
3. For B-type: defer to the next relevant Workshop session
4. Update the asset, mark the old version as Deprecated
5. Update all cross-references
6. Update CHANGELOG.md
7. Update ROADMAP.md
8. Perform full self-review before submission

### 7.3 Version Numbering

- MAJOR version: Breaking changes or fundamental restructuring
- MINOR version: New features, additions, or significant revisions
- PATCH version: Bug fixes, typos, or minor corrections

---

## 8. Workshop Documentation

Every Workshop session MUST produce a session-N.md file in `00_Governance/Workshop/`.

Each session file MUST include:

- Asset being discussed
- Key discussion points
- Decisions made (with IDs)
- Self-Review findings
- Next actions

---

## 9. Baseline Maintenance

After each milestone (M001, M002, M003, ...), the Chief Architect MUST:

1. Run full cross-document consistency audit
2. Update CHANGELOG.md with milestone summary
3. Update ROADMAP.md with current status
4. Update README.md asset inventory
5. Verify all Decision IDs are unique and contiguous
6. Verify all Cross-References are complete and bidirectional
7. Verify all assets have proper metadata headers

---

## 10. Self-Review Checklist (Quick Reference)

### Before Starting a Workshop Session

- [ ] Review existing assets for context
- [ ] Identify which frozen assets might be impacted
- [ ] Prepare draft asset structure

### During Asset Creation

- [ ] Update CM-003 first (if new terms introduced)
- [ ] Follow WF-002 §6 Asset Structure template
- [ ] Use correct Decision ID (check for uniqueness)
- [ ] Add Cross-References section

### Before Submitting for Review

- [ ] Terminology matches CM-003
- [ ] No contradiction with FP-001
- [ ] No violation of AP-001
- [ ] No conflict with CM-002
- [ ] No duplicate Decision IDs
- [ ] No stale references (grep verified)
- [ ] Version number incremented
- [ ] CHANGELOG.md updated
- [ ] Cross-references complete and bidirectional

### Before Freezing an Asset

- [ ] All decisions have unique IDs
- [ ] Cross-references are complete
- [ ] Self-review is documented
- [ ] Project Owner has reviewed

### Before Updating a Frozen Asset

- [ ] Impact scope assessed (which other assets affected?)
- [ ] Change classified (A-type or B-type)
- [ ] CM-003 updated first (if new terms)
- [ ] All affected documents updated (grep verified)
- [ ] Cross-references updated
- [ ] CHANGELOG.md updated
- [ ] Old version marked appropriately (Deprecated / superseded)

---

## Cross-References

- **WF-001** Architecture Workflow — These norms extend and enforce WF-001 rules
- **AP-001** Architecture Principles — These norms comply with all 13 principles
- **FP-001** CEAP Definition — These norms implement the platform definition
- **CM-003** Ubiquitous Language — These norms enforce terminology consistency
- **CM-002** Core Concept Model — These norms align with the concept model
