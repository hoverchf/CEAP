# PC-001 Project Charter

**Status:** Frozen
**Version:** v0.1
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## 1. Project Background

CEAP 建设的核心问题已在 **BS-001** 中明确：企业缺少一套能够持续沉淀、组织、复用和放大专家知识的统一平台。

专家能力存在于个人大脑中，不随人员流动而转移。新人成长周期长，相同问题重复分析，企业能力增长速度受限。

**CEAP 的解决方案：** 通过 Architecture-Driven Development，将专家经验转化为可持续积累的知识资产，构建 Enterprise Communication Knowledge Platform。

---

## 2. Project Scope

### In Scope

| Phase | 内容 | 核心资产 |
|-------|------|---------|
| **Phase 1: Foundation** | 治理层建设 | AP-001, FP-001, VF-001, BS-001 |
| **Phase 2: Domain Model** | 概念模型与语言 | CM-002, CM-003, B-001, ADR-001/002/003 |
| **Phase 3: Architecture** | 详细架构设计 | PC-001, VS-001, AR-001, DM-001 |
| **Phase 4+: Engineering** | 工程实现 | 01_Knowledge, 02_Engineering, 03_Runtime |

### Out of Scope

- 产品功能开发
- 日常运维监控

---

## 3. Organizational Structure

### Core Team (~10 people)

| Role | Responsibilities | Headcount |
|------|-----------------|-----------|
| **Project Owner** | 领域专家，最终决策者，资产 Reviewer | 1 |
| **Chief Architect** | 架构设计、资产产出、自我审查、跨资产一致性 | 1 |
| **Domain Experts** | 提供领域知识，参与 Workshop，验证分析流程 | 2-3 |
| **Engineers** | 工程实现（Phase 4+） | 2-3 |
| **AI Developers** | AI Agent / Reasoning Model 开发（Phase 4+） | 1-2 |
| **Field Testers** | 现场测试，提供初步分析数据 | 1-2 |

### Decision Mechanism

- **Architecture decisions:** Chief Architect drafts → Project Owner approves → Frozen
- **Domain knowledge:** Project Owner provides → Chief Architect converts to architecture assets
- **Dispute resolution:** Project Owner has final authority

---

## 4. Milestones

| Milestone | Trigger Condition | Status |
|-----------|------------------|--------|
| **M001: Bootstrap** | Repository initialized, README established | ✓ Completed |
| **M002: Architecture Foundation** | AP-001, FP-001, VF-001, BS-001, CM-001, ADR-001/002/003 | ✓ Completed |
| **M003: Domain Model Baseline** | CM-002, CM-003, B-001, WF-001 completed, assets standardized | ✓ Completed |
| **M004: Vision & Charter** | VS-001, PC-001 completed | In Progress |
| **M005: Architecture Design** | AR-001, DM-001 completed | Pending |
| **M006: Engineering** | 01_Knowledge, 02_Engineering, 03_Runtime started | Pending |

---

## 5. Value Assessment Framework

Per **VF-001**, CEAP does not use Success Criteria. Instead, we evaluate investment value through the Value Framework at each phase gate.

### Phase Gate Evaluation Criteria

| Phase | Evaluation Dimension | Evaluation Method |
|-------|---------------------|-------------------|
| **Phase 1-2** (Foundation + Domain Model) | Architecture baseline stability | Asset Freeze pass rate, cross-reference integrity, Decision ID uniqueness |
| **Phase 3** (Detailed Architecture) | Design executability | Design review pass rate, consistency with concept model, principle compliance |
| **Phase 4+** (Engineering + Runtime) | Value realization | Efficiency improvement, quality improvement, knowledge asset accumulation rate, new expert growth cycle |

### Evaluation Checklist (per WF-001 §9)

Before each Phase Gate:

- [ ] All assets in that phase are Frozen
- [ ] Cross-references are consistent (CM-003 terminology compliance)
- [ ] Self-review has been performed on each asset
- [ ] No asset contradicts FP-001 or violates AP-001
- [ ] All capabilities map to VF-001
- [ ] CHANGELOG.md is updated
- [ ] ROADMAP.md reflects current status

---

## 6. Working Method

### Workshop-Driven Evolution

Per **AP-001 Principle 7** and **WF-001 §1**:

```
Workshop (discussion + consensus)
    ↓
Self-Review (architect proactively corrects)
    ↓
Asset Production (formal documentation)
    ↓
Architecture Freeze (Project Owner approval)
    ↓
Repository (baseline commit)
```

### Self-Review Discipline

Per **WF-001 §3**:

- Self-review is mandatory before submitting any asset for review
- Architect must check: terminology drift, structural inconsistency, over-abstraction, missing concepts, false equivalences, premature freezing
- Discoveries classified as A-type (freeze immediately) or B-type (defer to broader review)

---

## 7. Cross-References

- **FP-001** CEAP Definition — Charter implements the platform definition
- **VS-001** Vision Statement — Charter operationalizes the vision
- **VF-001** Value Framework — Value Assessment Framework maps to this
- **BS-001** Current State — Project background sourced from this
- **AP-001** Architecture Principles — Charter complies with all principles
- **CM-002** Core Concept Model — Charter scope aligns with domain model
- **WF-001** Architecture Workflow — Charter follows this workflow
