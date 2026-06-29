# ADR-007 Knowledge Asset Schema

**Status:** Accepted
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Context

From **AR-001 §2.3** and **DM-001 §14**: Knowledge Assets are the Case's final value output. CEAP defines 9 types of knowledge assets.

This document defines the data schema for each asset type.

---

## Decision

### P0 Asset Types (Directly Serve Agent Analysis)

#### 1. SOP (Standard Operating Procedure)

| Field | Type | Description |
|-------|------|-------------|
| `sop_id` | UUID | Unique identifier |
| `title` | String | SOP title |
| `steps` | List\<SOPStep\> | Ordered procedure steps |
| `applicable_scenarios` | List\<String\> | When to use this SOP |
| `created_from_case` | UUID | Source Case ID |
| `version` | String | Version number |
| `confirmed_by` | String | Confirming expert |
| `tags` | List\<String\> | Search tags |

**SOPStep:**
| Field | Type | Description |
|-------|------|-------------|
| `order` | Integer | Step number |
| `action` | String | What to do |
| `expected_result` | String | What should happen |
| `tools_required` | List\<String\> | Tools needed |

#### 2. Workflow

| Field | Type | Description |
|-------|------|-------------|
| `workflow_id` | UUID | Unique identifier |
| `title` | String | Workflow title |
| `stages` | List\<Stage\> | Workflow stages |
| `applicable_scenarios` | List\<String\> | When to use |
| `created_from_case` | UUID | Source Case ID |
| `version` | String | Version number |
| `confirmed_by` | String | Confirming expert |
| `tags` | List\<String\> | Search tags |

**Stage:**
| Field | Type | Description |
|-------|------|-------------|
| `order` | Integer | Stage order |
| `name` | String | Stage name |
| `reasoning_models` | List\<String\> | Recommended Reasoning Models |
| `output` | String | Expected output |

#### 3. Skills

| Field | Type | Description |
|-------|------|-------------|
| `skill_id` | UUID | Unique identifier |
| `name` | String | Skill name |
| `description` | String | What the skill does |
| `input_type` | String | Expected input format |
| `output_type` | String | Output format |
| `reasoning_model` | String | Associated Reasoning Model |
| `created_from_case` | UUID | Source Case ID |
| `version` | String | Version number |
| `confirmed_by` | String | Confirming expert |
| `tags` | List\<String\> | Search tags |

#### 4. Evidence Pattern

| Field | Type | Description |
|-------|------|-------------|
| `pattern_id` | UUID | Unique identifier |
| `name` | String | Pattern name |
| `evidence_combination` | List\<EvidenceCondition\> | Evidence conditions that form this pattern |
| `associated_finding` | String | Finding this pattern typically leads to |
| `confidence` | Float | Historical accuracy |
| `occurrence_count` | Integer | How many times observed |
| `created_from_case` | UUID | Source Case ID |
| `version` | String | Version number |
| `confirmed_by` | String | Confirming expert |
| `tags` | List\<String\> | Search tags |

**EvidenceCondition:**
| Field | Type | Description |
|-------|------|-------------|
| `evidence_type` | Enum | AP_LOG / MODEM_LOG / NET_LOG / VIDEO / ... |
| `condition` | String | Match condition (e.g., "retransmission > 2%") |
| `weight` | Float | Relative importance in pattern |

#### 5. Root Cause Pattern

| Field | Type | Description |
|-------|------|-------------|
| `pattern_id` | UUID | Unique identifier |
| `name` | String | Pattern name |
| `root_cause` | String | Root cause description |
| `evidence_chain` | List\<ChainNode\> | Complete evidence chain (from DM-001 §5) |
| `associated_problem_family` | UUID | Related Problem Family |
| `confidence` | Float | Historical accuracy |
| `occurrence_count` | Integer | How many times confirmed |
| `created_from_case` | UUID | Source Case ID |
| `version` | String | Version number |
| `confirmed_by` | String | Confirming expert |
| `tags` | List\<String\> | Search tags |

### P1 Asset Types (Supporting Assets)

#### 6. Methodology

| Field | Type | Description |
|-------|------|-------------|
| `methodology_id` | UUID | Unique identifier |
| `name` | String | Methodology name |
| `description` | String | Methodology description |
| `reasoning_models` | List\<String\> | Recommended Reasoning Models |
| `applicable_scenarios` | List\<String\> | When to use |
| `created_from_case` | UUID | Source Case ID |
| `version` | String | Version number |
| `confirmed_by` | String | Confirming expert |
| `tags` | List\<String\> | Search tags |

#### 7. Expert Experience

| Field | Type | Description |
|-------|------|-------------|
| `experience_id` | UUID | Unique identifier |
| `expert_name` | String | Expert who contributed |
| `content` | String | Experience description |
| `context` | String | When and how this experience applies |
| `created_from_case` | UUID | Source Case ID |
| `version` | String | Version number |
| `confirmed_by` | String | Confirming expert |
| `tags` | List\<String\> | Search tags |

#### 8. Reasoning Model (Stored as Asset)

| Field | Type | Description |
|-------|------|-------------|
| `model_asset_id` | UUID | Unique identifier |
| `model_name` | String | Reasoning Model name |
| `model_config` | Object | Model configuration parameters |
| `success_rate` | Float | Historical success rate |
| `applicable_scenarios` | List\<String\> | When to use |
| `created_from_case` | UUID | Source Case ID |
| `version` | String | Version number |
| `confirmed_by` | String | Confirming expert |
| `tags` | List\<String\> | Search tags |

#### 9. Test Case Template

| Field | Type | Description |
|-------|------|-------------|
| `template_id` | UUID | Unique identifier |
| `name` | String | Template name |
| `test_steps` | List\<String\> | Test procedure steps |
| `expected_evidence` | List\<EvidenceCondition\> | Expected evidence to collect |
| `applicable_scenarios` | List\<String\> | When to use |
| `created_from_case` | UUID | Source Case ID |
| `version` | String | Version number |
| `confirmed_by` | String | Confirming expert |
| `tags` | List\<String\> | Search tags |

---

## Consequences

1. All 9 asset types have standardized schemas.
2. P0 assets (SOP, Workflow, Skills, Evidence Pattern, Root Cause Pattern) directly serve Agent analysis.
3. P1 assets support methodology evolution and expert knowledge preservation.
4. All assets are versioned and traceable to source Case.
5. Expert confirmation required for all assets (Agent extracts, expert confirms).

---

## Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-091 | 9 knowledge asset types standardized | Frozen |
| D-092 | P0: SOP, Workflow, Skills, Evidence Pattern, Root Cause Pattern | Frozen |
| D-093 | P1: Methodology, Expert Experience, Reasoning Model, Test Case Template | Frozen |
| D-094 | All assets versioned and traceable to source Case | Frozen |
| D-095 | Agent auto-extracts, expert confirms | Frozen |
| D-096 | Evidence Pattern includes weight for relative importance | Frozen |
| D-097 | Root Cause Pattern includes complete evidence chain | Frozen |
| D-098 | Skills associated with Reasoning Model | Frozen |
| D-099 | Test Case Template defines expected evidence to collect | Frozen |

---

## Cross-References

- **AR-001** Architecture Design — §2.3 Knowledge Asset Management
- **DM-001** Domain Model — §14 Knowledge Asset entity
- **CM-003** Ubiquitous Language — Knowledge Assets definition
- **ADR-004** Reasoning Model Architecture — Skills associated with Models
- **ADR-008** Structured Output Document — Knowledge Assets extracted from reports
