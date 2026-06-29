# Session-012 — Architecture Baseline Review

**Asset:** WF-001
**Asset Name:** Architecture Baseline Review
**Status:** Draft

---

## 讨论主题

从 M003 基线（session-1 ~ session-9）到当前（session-10 ~ session-11），检查已冻结资产是否需要更新。

---

## 冻结资产清单

| 资产 | 状态 | 受影响？ |
|------|------|---------|
| AP-001 | Approved | 否 |
| FP-001 | Frozen | 否 |
| VF-001 | Freeze Candidate | 否 |
| BS-001 | Freeze Candidate | 否 |
| ADR-001 | Accepted | 否 |
| ADR-002 | Accepted | 否 |
| ADR-003 | Accepted | 否 |
| CM-002 | Freeze Candidate | **是** |
| CM-003 | Freeze Candidate | **是** |
| B-001 | Frozen | 否 |
| WF-001 | Freeze Candidate | 否 |

---

## 需要更新的资产

### CM-002 — Core Concept Model

**变更：新增 Problem Family**

CM-002 的顶层模型需要增加 Problem Family 层级：

```
Problem Family
    └── Analysis Case (聚合根)
            ├── Analysis Session
            ├── Evidence
            ├── Investigation
            ├── Agent
            ├── Harness
            ├── Observation
            ├── Hypothesis
            ├── Finding
            ├── Root Cause
            └── Knowledge Assets
```

**变更：新增 Session 实体**

CM-002 中 Session 之前被错误地标记为"已取消"，现已恢复。

### CM-003 — Ubiquitous Language

**变更：新增 Problem Family 定义**

CM-003 需要补充 Problem Family 的统一定义。

**变更：修正 Session 定义**

CM-003 中 Session 的定义需要确认与 DM-001 一致（Session 是系统操作的最小实体，Team 是管理组织方式）。

---

## 不需要更新的资产

- **AP-001** — 13 条原则不受影响
- **FP-001** — 平台定义不受影响
- **VF-001** — 价值框架不受影响
- **BS-001** — 现状分析不受影响
- **ADR-001** — Analysis Case 决策不受影响
- **ADR-002** — Reasoning Framework 决策不受影响
- **ADR-003** — Evidence-Driven Analysis 决策不受影响
- **B-001** — Investigation & Classification 不受影响
- **WF-001** — Architecture Workflow 不受影响

---

## 决策

| ID | Decision | Status |
|----|----------|--------|
| D-056 | CM-002 需要更新，增加 Problem Family 层级 | Pending |
| D-057 | CM-003 需要更新，增加 Problem Family 定义 | Pending |
| D-058 | 其他已冻结资产不需要更新 | Frozen |

---

## Self-Review

本次 review 发现 CM-002 和 CM-003 需要更新。这两个资产都是 Freeze Candidate 状态，更新成本较低。

**关键提醒：** 如果后续有变更影响到 Frozen 状态的资产，必须走正式的更新流程（WF-001 §4.4）。

---

## 后续行动

- 更新 CM-002（增加 Problem Family）
- 更新 CM-003（增加 Problem Family 定义）
- 提交 CM-002/003 评审
