# DM-001 Domain Model

**Status:** Frozen
**Version:** v0.5
**Created:** 2026-06-27
**Updated:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## 1. Domain Model Overview

DM-001 从 CM-002 的概念模型落地到实现级别的领域模型。

**核心关系：**

```
Problem Family (问题家族)
    └── Analysis Case (聚合根)
            ├── Analysis Session (实体)
            ├── Evidence (实体)
            ├── Investigation (值对象)
            ├── Agent (实体)
            ├── Harness (实体)
            ├── Observation (实体)
            ├── Hypothesis (实体)
            ├── Finding (实体)
            ├── Root Cause (实体)
            └── Knowledge Assets (实体集合)
```

**关键理解：**

- **Problem Family** 是 Case 的上层分类。一类问题（Problem Family）包含多个 Case，同一个 Problem Family 下的 Case 共享分析方法论和知识资产。
- **Analysis Session** 是 Case 内的一次分析活动。Agent 是 Session 的执行主体，但 Session 作为"分析活动"的概念仍然存在。
- **Session 是系统操作的最小实体**，Team 是公司管理组织方式。
- **Session 是团队间传递分析结果的载体** — 团队间不直接传递，而是通过 Session 的输出传递。
- **一个团队可以有多个 Session，但一个 Session 只属于一个团队。**
- **一个团队的工作由一个或多个 Session 执行。**

---

## 2. Problem Family — 实体

### 2.1 定义

Problem Family 是 Case 的上层分类。

一类问题（Problem Family）包含多个 Case。同一个 Problem Family 下的 Case 可以互相参考。

### 2.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `family_id` | UUID | 问题家族唯一标识 |
| `name` | String | 问题家族名称（如"WhatsApp 图片发送延迟"） |
| `description` | String | 问题家族描述 |
| `category` | String | 分类（如"OTT 应用"、"信令流程"、"网络性能"） |
| `analysis_methodology` | String | 家族共享的分析方法论 |
| `associated_case_ids` | List\<UUID\> | 关联的 Case ID |
| `shared_knowledge_assets` | List\<UUID\> | 家族共享的知识资产 |
| `created_at` | DateTime | 创建时间 |
| `updated_at` | DateTime | 更新时间 |

### 2.3 不变量

- 一个 Problem Family 可以有多个 Case
- 一个 Case 属于且只属于一个 Problem Family
- Case 可以在不同 Problem Family 之间调整
- Problem Family 的分析方法论持续演进（基于 Case 的实际分析结果）
- Problem Family 共享知识资产（同一个 Family 的 Case 沉淀通用的 Knowledge Asset）

---

## 3. Analysis Case — 聚合根

### 3.1 定义

Analysis Case 是 CEAP 中唯一的聚合根（Aggregate Root）。

所有其他领域对象都属于 Case，不能独立存在。

### 3.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `case_id` | UUID | Case 唯一标识 |
| `family_id` | UUID | 所属问题家族 |
| `problem_description` | String | 问题描述 |
| `metadata` | Map | 元数据（创建时间、负责人、标签等） |
| `status` | Enum | Problem Reported / Evidence Collected / Analysis In Progress / Root Cause Confirmed / Knowledge Extracted / Closed |
| `sessions` | List\<AnalysisSession\> | 分析活动集合 |
| `investigations` | List\<Investigation\> | 调查记录 |
| `evidences` | List\<Evidence\> | 证据集合 |
| `observations` | List\<Observation\> | 观察记录 |
| `hypotheses` | List\<Hypothesis\> | 假设集合 |
| `findings` | List\<Finding\> | 推理结论 |
| `root_cause` | RootCause | 根因（一个 Case 只有一个） |
| `root_cause_evidence_chain` | EvidenceChain | 根因的证据链 |
| `knowledge_assets` | List\<KnowledgeAsset\> | 知识资产集合 |
| `created_at` | DateTime | 创建时间 |
| `closed_at` | DateTime | 关闭时间 |

### 3.3 不变量

- 一个业务问题对应一个 Case
- 一个 Case 属于且只属于一个 Problem Family
- 一个 Case 可以有多个 Analysis Session
- 一个 Case 可以有多个 Investigation
- 一个 Case 可以有多个 Evidence
- 一个 Case 可以有多个 Observation
- 一个 Case 可以有多个 Hypothesis
- 一个 Case 可以有多个 Finding
- 一个 Case 只有一个 Root Cause
- 一个 Case 只有一个 Root Cause Evidence Chain
- 一个 Case 可以有多个 Knowledge Assets
- **Evidence 是不可变的** — 一旦创建不能被修改
- **Session 是团队间传递分析结果的载体**

---

## 4. Analysis Session — 实体

### 4.1 定义

Analysis Session 是 Case 内的一次分析活动。

Session 由 Agent 执行（Agent 是执行主体），但 Session 本身是"分析活动"的概念。

Session 是系统操作的最小实体。

### 4.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `session_id` | UUID | Session 唯一标识 |
| `case_id` | UUID | 所属 Case |
| `team_id` | UUID | 所属团队（Application/Performance/Platform/Protocol） |
| `agent_id` | UUID | 执行的 Agent |
| `purpose` | String | Session 目的（如"排查 AP 层异常"） |
| `input_evidence_ids` | List\<UUID\> | 输入的 Evidence |
| `input_findings` | List\<UUID\> | 输入的 Finding（来自其他团队） |
| `output_observations` | List\<UUID\> | 输出的 Observation |
| `output_findings` | List\<UUID\> | 输出的 Finding |
| `output_investigations` | List\<UUID\> | 触发的 Investigation |
| `status` | Enum | Started / In Progress / Completed / Terminated |
| `created_at` | DateTime | 创建时间 |
| `completed_at` | DateTime | 完成时间 |

### 4.3 Session 的生命周期

```
Session Start
    ↓
Consume Evidence (从 Case 读取)
    ↓
Consume Input Findings (来自其他团队)
    ↓
Generate Observation (Agent 执行)
    ↓
Generate / Update Hypothesis
    ↓
Reasoning (通过 Reasoning Model)
    ↓
Produce Finding
    ↓
Trigger Investigation (如需新 Evidence)
    ↓
Session Result (输出到 Case)
    ↓
Next Session (Optional)
```

### 4.4 Session 的团队传递

Session 是团队间传递分析结果的载体：

```
Team A Session 完成
    ↓
输出 Finding
    ↓
触发 Investigation（可由 Team A 或 Team B 执行）
    ↓
Team B 接收 Investigation 结果
    ↓
Team B 启动新 Session
    ↓
Team B 分析 Investigation 结果 + 共享 Evidence
    ↓
输出新的 Finding
    ↓
...
```

---

## 5. Evidence — 实体

### 5.1 定义

Evidence 是客观事实，属于 Case，不可变。

### 5.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `evidence_id` | UUID | 证据唯一标识 |
| `case_id` | UUID | 所属 Case |
| `type` | Enum | AP_LOG / MODEM_LOG / NET_LOG / VIDEO / SCREENSHOT / COUNTER / CONFIGURATION / TEST_RESULT / AI_ANALYSIS_RESULT |
| `platform` | Enum | MTK / QUALCOMM / OTHER |
| `source` | String | 数据来源 |
| `size_bytes` | Long | 文件大小 |
| `upload_time` | DateTime | 上传时间 |
| `storage_path` | String | 存储路径 |
| `annotation` | String | 测试人员标注的重点区域 |
| `created_by` | String | 采集者 |

### 5.3 不变量

- Evidence 属于 Case，不属于任何 Agent 或专家
- Evidence 不可变
- 多个 Agent 可以共享同一个 Evidence

---

## 6. Root Cause Evidence Chain — 实体

### 6.1 定义

Root Cause Evidence Chain 是 Root Cause 的完整证据链。

它记录了从 Root Cause 回溯到所有支撑 Evidence 的完整链路。

### 6.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `chain_id` | UUID | 证据链唯一标识 |
| `case_id` | UUID | 所属 Case |
| `root_cause_id` | UUID | 关联的 Root Cause |
| `chain` | List\<ChainNode\> | 证据链节点列表 |

### 6.3 ChainNode 结构

```
ChainNode
    ├── type: ENUM (EVIDENCE / OBSERVATION / HYPOTHESIS / FINDING)
    ├── id: UUID
    ├── content: String
    ├── supporting_ids: List\<UUID\> (父节点 ID)
    └── confidence: Float (0.0 - 1.0)
```

**示例：**

```
Root Cause: WiFi AP 异常
    └── Finding: 网络存在轻微丢包 (confidence=0.85)
        └── Finding: 重传率偏高 (confidence=0.90)
            └── Observation: 重传率略高 (confidence=0.95)
                └── Evidence: TCP Retransmission = 3% (confidence=1.0)
```

---

## 7. Investigation — 值对象

### 7.1 定义

Investigation 是真实世界的活动，用于获取新 Evidence。

### 7.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `investigation_id` | UUID | 调查唯一标识 |
| `case_id` | UUID | 所属 Case |
| `triggered_by` | String | 触发者（Agent 或专家） |
| `request` | String | 调查请求（如"抓取 CPU Profile"） |
| `target` | String | 调查目标（如"Server"、"Client"） |
| `assigned_team` | String | 执行团队（Application/Performance/Platform/Protocol） |
| `status` | Enum | Pending / In Progress / Completed |
| `result_evidence_ids` | List\<UUID\> | 产生的 Evidence ID |
| `created_at` | DateTime | 创建时间 |
| `completed_at` | DateTime | 完成时间 |

---

## 8. Agent — 实体

### 8.1 定义

Agent 是 CEAP 的主力分析执行者。

### 8.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `agent_id` | UUID | Agent 唯一标识 |
| `name` | String | Agent 名称 |
| `reasoning_model` | String | 当前使用的 Reasoning Model |
| `confidence_threshold` | Float | 置信度阈值 |
| `learning_context` | LearningContext | 当前 Case 内的学习上下文 |
| `status` | Enum | Idle / Running / Paused / Terminated |

### 8.3 学习上下文（LearningContext）

| 字段 | 类型 | 说明 |
|------|------|------|
| `case_id` | UUID | 当前 Case |
| `hypotheses_tried` | List\<String\> | 尝试过的假设 |
| `hypotheses_eliminated` | List\<String\> | 排除的假设及原因 |
| `findings_produced` | List\<String\> | 产生的结论 |
| `expert_corrections` | List\<Correction\> | 专家纠正记录 |

**注意：** 学习上下文仅限于当前 Case，不跨 Case 复用。

---

## 9. Harness — 实体

### 9.1 定义

Harness 是控制 Agent 行为的操作系统。

### 9.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `harness_id` | UUID | Harness 唯一标识 |
| `case_id` | UUID | 所属 Case |
| `agent_id` | UUID | 关联的 Agent |
| `control_events` | List\<ControlEvent\> | 控制事件记录 |
| `validation_results` | List\<ValidationResult\> | 校验结果记录 |
| `manual_overrides` | List\<ManualOverride\> | 专家手动介入记录 |

### 9.3 控制事件（ControlEvent）

| 字段 | 类型 | 说明 |
|------|------|------|
| `event_id` | UUID | 事件唯一标识 |
| `timestamp` | DateTime | 事件时间 |
| `type` | Enum | DIRECTION_SET / PAUSED / RESUMED / TERMINATED / BEHAVIOR_TUNED |
| `actor` | String | 操作者（专家） |
| `details` | String | 事件详情 |

### 9.4 手动介入（ManualOverride）

| 字段 | 类型 | 说明 |
|------|------|------|
| `override_id` | UUID | 介入唯一标识 |
| `timestamp` | DateTime | 介入时间 |
| `action` | Enum | ADD_OBSERVATION / CORRECT_FINDING / SPECIFY_DIRECTION / INJECT_EVIDENCE |
| `details` | String | 介入详情 |

---

## 10. Observation — 实体

### 10.1 定义

Observation 是专家或 Agent 对 Evidence 的解释。

### 10.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `observation_id` | UUID | 观察唯一标识 |
| `case_id` | UUID | 所属 Case |
| `evidence_ids` | List\<UUID\> | 引用的 Evidence |
| `content` | String | 观察内容 |
| `generated_by` | Enum | AGENT / EXPERT / MANUAL_OVERRIDE |
| `session_id` | UUID | 所属 Session |
| `team_id` | UUID | 所属团队 |
| `confidence` | Float | 置信度（0.0 - 1.0） |
| `created_at` | DateTime | 创建时间 |

---

## 11. Hypothesis — 实体

### 11.1 定义

Hypothesis 是 tentative explanation，连接 Evidence 和 Reasoning。

### 11.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `hypothesis_id` | UUID | 假设唯一标识 |
| `case_id` | UUID | 所属 Case |
| `content` | String | 假设内容 |
| `supporting_observations` | List\<UUID\> | 支持的 Observation |
| `status` | Enum | ACTIVE / UPDATING / ELIMINATED |
| `elimination_reason` | String | 排除原因（如果已排除） |
| `generated_by` | Enum | AGENT / EXPERT |
| `session_id` | UUID | 所属 Session |
| `team_id` | UUID | 所属团队 |
| `created_at` | DateTime | 创建时间 |
| `updated_at` | DateTime | 更新时间 |

---

## 12. Finding — 实体

### 12.1 定义

Finding 是经过推理后的结论，支持证据链。

### 12.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `finding_id` | UUID | 结论唯一标识 |
| `case_id` | UUID | 所属 Case |
| `content` | String | 结论内容 |
| `supporting_evidence_ids` | List\<UUID\> | 支撑的 Evidence |
| `supporting_observation_ids` | List\<UUID\> | 支撑的 Observation |
| `supporting_hypothesis_ids` | List\<UUID\> | 支撑的 Hypothesis |
| `confidence` | Float | 置信度（0.0 - 1.0） |
| `generated_by` | Enum | AGENT / EXPERT / MANUAL_OVERRIDE |
| `session_id` | UUID | 所属 Session |
| `team_id` | UUID | 所属团队 |
| `created_at` | DateTime | 创建时间 |

---

## 13. Root Cause — 实体

### 13.1 定义

Root Cause 是有证据支撑的根本原因。

### 13.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `root_cause_id` | UUID | 根因唯一标识 |
| `case_id` | UUID | 所属 Case |
| `content` | String | 根因描述 |
| `supporting_finding_ids` | List\<UUID\> | 支撑的 Finding |
| `evidence_chain_id` | UUID | 关联的 Root Cause Evidence Chain |
| `confidence` | Float | 置信度（0.0 - 1.0） |
| `confirmed_by` | String | 确认专家 |
| `confirmed_at` | DateTime | 确认时间 |

---

## 14. Knowledge Asset — 实体集合

### 14.1 定义

Knowledge Assets 是 Case 的最终价值输出。

### 14.2 字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `asset_id` | UUID | 资产唯一标识 |
| `case_id` | UUID | 所属 Case |
| `type` | Enum | METHODOLOGY / WORKFLOW / SOP / SKILLS / EVIDENCE_PATTERN / ROOT_CAUSE_PATTERN / EXPERT_EXPERIENCE / REASONING_MODEL / TEST_CASE_TEMPLATE |
| `content` | String / Document | 资产内容 |
| `version` | String | 版本号 |
| `extracted_by` | Enum | AGENT / EXPERT |
| `confirmed_by` | String | 确认专家 |
| `confirmed_at` | DateTime | 确认时间 |
| `tags` | List\<String\> | 标签 |

---

## 15. Multi-Team Collaboration — 领域模型

### 15.1 团队模型

```
Analysis Case
    └── Sessions (多团队分析活动)
            ├── Application Team Sessions
            │       └── Session #1: 分析 AP Log
            │       └── Session #2: 分析 Investigation 结果
            ├── Performance Team Sessions
            │       └── Session #1: 分析性能指标
            ├── Platform Team Sessions
            │       └── Session #1: 分析系统层
            └── Protocol Team Sessions
                    └── Session #1: 分析 Modem/Net Log
```

### 15.2 团队协作规则

- **并行：** 各团队可以同时启动 Session，各自分析自己模块
- **串行：** 一个 Session 的输出（Finding / Investigation Request）可以触发另一个团队的 Session
- **共享：** 所有团队共享同一个 Case 的 Evidence Store
- **传递：** 团队间的传递通过 Session 的输出实现

### 15.3 团队协作流程

```
[并行]
App Team Session #1 → 输出 Finding: "AP 层无异常"
Perf Team Session #1 → 输出 Finding: "性能指标正常"
Proto Team Session #1 → 输出 Finding: "网络有丢包"

[触发 Investigation]
Proto Team Session #1 → 触发 Investigation: "抓取 WiFi AP 配置"

[串行]
Investigation 完成 → 新 Evidence 进入 Case
Proto Team Session #2 → 分析新 Evidence → 输出 Finding: "WiFi AP 配置异常"

[汇总]
所有 Session 的 Finding 汇总 → Root Cause: "WiFi AP 异常"
```

---

## 16. Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-042 | Analysis Case 是唯一的聚合根 | Frozen |
| D-043 | Evidence 是不可变实体 | Frozen |
| D-044 | Agent 学习限于当前 Case | Frozen |
| D-045 | Harness 是控制 Agent 的实体，不是值对象 | Frozen |
| D-046 | Analysis Session 是团队间传递分析结果的载体 | Frozen |
| D-047 | 多团队分析既有并行也有串行，通过 Session 传递 | Frozen |
| D-048 | Knowledge Asset 提取由 Agent 自动执行 + 专家确认 | Frozen |
| D-049 | 每个领域对象都有置信度（Confidence）字段 | Frozen |
| D-050 | 所有 Observation / Finding 记录所属 Session 和团队 | Frozen |
| D-051 | Root Cause 必须有完整的 Evidence Chain | Frozen |
| D-052 | Problem Family 是 Case 的上层分类 | Frozen |
| D-053 | Session 是系统操作的最小实体，Team 是管理组织方式 | Frozen |
| D-054 | 一个团队可以有多个 Session，一个 Session 只属于一个团队 | Frozen |
| D-055 | Problem Family 维护共享的分析方法论和知识资产 | Frozen |

---

## 17. Cross-References

- **CM-002** Core Concept Model — 领域模型基于此概念模型
- **CM-003** Ubiquitous Language — Agent, Harness, Team, Problem Family defined in CM-003
- **AR-001** Architecture Design — 领域模型实现架构设计
- **ADR-001** Analysis Case — Case 作为核心域对象的决策
- **ADR-002** Reasoning Framework — Hypothesis 和 Finding 与推理模型的关系
- **ADR-003** Evidence-Driven Analysis — Evidence 不可变性的决策
- **B-001** Investigation & Classification — Investigation 和 Four-Type Classification
- **VS-001** Vision Statement — 领域模型支持 Vision 目标
- **VF-001** Value Framework — 领域模型服务于价值创造
- **WF-001** Architecture Workflow — 领域模型的开发遵循此工作流
