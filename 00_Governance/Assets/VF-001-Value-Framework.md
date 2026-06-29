# VF-001 Value Framework

**Status:** Frozen
**Version:** v0.1
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## 1. Purpose

CEAP 的目标不是交付一个 AI 系统，也不是建设一个知识库。

CEAP 的目标是持续创造企业价值。

因此，平台中所有能力、所有工具、所有 AI、所有知识资产，都必须能够映射到统一的价值框架（Value Framework）。

Value Framework 是 CEAP 进行架构设计、能力规划、路线规划、价值评估和投资决策的统一依据。

---

## 2. Design Principle

CEAP 不采用 Success Criteria。

**原因：**

- Success 是项目视角。
- Value 是企业视角。
- CEAP 属于 Enterprise Architecture。

因此采用 Value Framework 作为最高价值模型。

---

## 3. Value Hierarchy

```
Operational Value
    ├── Efficiency
    └── Quality

            ↓

Knowledge Value
    └── Knowledge Assets

            ↓

Enterprise Value
    └── Enterprise Capability
```

**说明：**

- **Operational Value** 是直接价值（Efficiency 和 Quality 并列，非先后关系）。
- **Knowledge Value** 是可持续价值。
- **Enterprise Capability** 是最终价值。

---

## 4. Value Definition

### V1. Efficiency Value

**目标：** 提升专家真正用于分析的时间占比。

不仅包含分析速度，更重要的是消除所有分析前、分析中、分析后的低价值工作。

**消除的低价值工作包括：**

- Log 上传下载
- 数据整理
- 视频时间统计
- 数据格式转换
- 重复查询
- 重复验证

**本质：** 让专家时间用于推理，而不是机械劳动。

---

### V2. Quality Value

**目标：** 提升分析数据和分析结果的可信度。

**Quality 包括：**

**数据质量：**

- 时间准确
- 数据完整
- 数据一致

**分析质量：**

- 推理正确
- 证据充分
- 可复现
- 可解释

**最终效果：**

- 减少人工反复确认
- 减少专家之间分析差异

---

### V3. Knowledge Value

**目标：** 一次分析，永久沉淀。

**Knowledge Value 包括：**

- 分析流程
- 推理方法
- Evidence Pattern
- Root Cause Pattern
- Expert Experience

这些资产可以不断积累，不会因为人员流动而消失。

**核心认知：** 知识本身不是企业价值，知识资产化才是企业价值。

---

### V4. Enterprise Capability

**这是 CEAP 唯一最终目标。**

**企业能力不是：**

- 专家能力 × 专家人数

**而是：**

- 平台持续放大专家能力

**表现为：**

- 新专家成长更快
- AI 能承担重复分析
- 平台能够复用历史经验
- 企业能力持续提升

因此，Enterprise Capability 是 Value Framework 的最终输出。

---

## 5. Value Evolution

CEAP 的价值不是同时产生，而是逐步演进。

```
Tool
    ↓
Efficiency
    ↓
Quality
    ↓
Knowledge Assets
    ↓
Enterprise Capability
```

**阶段说明：**

| 阶段 | 重点 | 价值类型 |
|------|------|----------|
| 第一阶段 | 创造 Efficiency | Operational Value |
| 第二阶段 | 沉淀 Knowledge | Knowledge Value |
| 第三阶段 | 形成 Enterprise Capability | Enterprise Value |

**说明：** 虽然 Hierarchy 图中 Efficiency 和 Quality 是并列的，但在价值演进路径上，Efficiency 通常先于 Quality 显现，因为消除低价值工作是提升数据质量的前提。

**结论：** Roadmap 必须遵循这一价值演进。

---

## 6. Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-005 | CEAP 采用 Value Framework，而非 Success Criteria | Frozen |
| D-006 | 企业价值分为 Operational、Knowledge、Enterprise 三层 | Frozen |

> **Note:** "Knowledge" in D-006 refers to the Knowledge Value layer. The term for assets is "Knowledge Assets" per CM-003.
| D-007 | Enterprise Capability 是 CEAP 唯一最终价值目标 | Frozen |
| D-008 | 所有能力建设必须能够映射到 Value Framework | Frozen |

---

## Cross-References

- **FP-001** CEAP Definition — 核心价值链与此价值框架对齐
- **BS-001** Current State — 六大挑战分别映射到不同的价值层级
- **AP-001** Architecture Principles — 原则约束所有价值创造活动
- **CM-002** Core Concept Model — 概念模型服务于价值创造
- **ROADMAP** (non-asset) — 路线图遵循此价值演进顺序
