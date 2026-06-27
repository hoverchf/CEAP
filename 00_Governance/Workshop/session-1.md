# Session-001 — Value Framework

**Asset:** VF-001
**Asset ID:** VF-001
**Asset Name:** Value Framework
**Status:** Stable (Freeze Candidate)

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

- **Operational Value** 是直接价值。
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
| 第一阶段 | 重点创造 Efficiency | Operational Value |
| 第二阶段 | 重点沉淀 Knowledge | Knowledge Value |
| 第三阶段 | 形成 Enterprise Capability | Enterprise Value |

**结论：** Roadmap 也必须遵循这一价值演进。

---

## 6. Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-005 | CEAP 采用 Value Framework，而非 Success Criteria | Frozen |
| D-006 | 企业价值分为 Operational、Knowledge、Enterprise 三层 | Frozen |
| D-007 | Enterprise Capability 是 CEAP 唯一最终价值目标 | Frozen |
| D-008 | 所有能力建设必须能够映射到 Value Framework | Frozen |

---

## 7. Self-Review

这一版比我们之前讨论时又前进了一步。有两个变化我认为是正确的：

**第一个变化：**

以前：

```
Efficiency
    ↓
Quality
    ↓
Knowledge
    ↓
Capability
```

现在变成：

```
Operational Value
    ├── Efficiency
    └── Quality
```

这更符合你的观点：Quality 并不是 Efficiency 的下一层，而是同一层面的价值。

**第二个变化：**

我们以前说 "Knowledge"，现在正式改成 "Knowledge Assets"。

因为：知识本身不是企业价值，知识资产化才是企业价值。

---

**建议状态：** Freeze Candidate。

如果你认可，我们将 VF-001 冻结，不再修改，并作为后续 PC-001、Roadmap、Architecture Principles 的引用资产，而不是重复编写。
