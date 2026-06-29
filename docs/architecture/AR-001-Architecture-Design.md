# AR-001 Architecture Design

**Status:** Frozen
**Version:** v0.3
**Created:** 2026-06-27
**Updated:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## 1. Architecture Overview

### 1.1 Four-Layer Architecture Design

CEAP 的系统架构分为四层，遵循 **FP-001** 定义的架构分层：

```
┌─────────────────────────────────────────────────────────────┐
│                    Business Layer                            │
│              Enterprise Communication Capability             │
│         (最终目标：企业通信问题分析能力的持续提升)              │
└─────────────────────────────────────────────────────────────┘
                              ▲
┌─────────────────────────────────────────────────────────────┐
│                   Platform Layer (CEAP)                      │
│                                                             │
│  ┌─────────────┐  ┌──────────────┐  ┌──────────────────┐   │
│  │  Data       │  │  Agent       │  │  Knowledge       │   │
│  │  Layer      │  │  Harness     │  │  Asset Mgmt      │   │
│  │             │  │              │  │                  │   │
│  │ 采集/存储/   │  │ Agent 自主   │  │ 知识资产自动提取  │   │
│  │ 传输/检索    │  │ 分析 + 专家  │  │ + 专家确认        │   │
│  │             │  │ 校验         │  │                  │   │
│  └─────────────┘  └──────────────┘  └──────────────────┘   │
│                                                             │
│  ─── Agent Harness 是平台的核心执行链路 ───                   │
│  ─── Agent 是主力分析执行者，专家通过结构化文档校验证据链      │
│  ─── 专家可随时手动介入，接管分析                            │
└─────────────────────────────────────────────────────────────┘
                              ▲
┌─────────────────────────────────────────────────────────────┐
│                  Capability Layer                            │
│  AI / Knowledge / Workflow / Automation / Tools              │
│  (Agent 使用的 Reasoning Model、Skills 等属于此层)            │
└─────────────────────────────────────────────────────────────┘
                              ▲
┌─────────────────────────────────────────────────────────────┐
│                     Data Layer                               │
│  Logs / Videos / Test Results / Documents                    │
│  (原始数据，即 Evidence 的来源)                                │
└─────────────────────────────────────────────────────────────┘
```

**四层职责映射：**

| 层 | 对应价值链环节 | 职责 | 类比 |
|----|--------------|------|------|
| **Data Layer** | Expertise（输入） | 采集和存储原始数据（Evidence） | 原料库 |
| **Platform Layer** | Platform（加工） | 将 Expertise 转化为 Knowledge Assets | 工厂 |
| **Capability Layer** | Knowledge Assets（输出） | AI、工具、Workflow 等能力 | 工具箱 |
| **Business Layer** | Enterprise Capability（目标） | 企业通信问题分析能力 | 产品 |

### 1.2 Agent Harness Design Philosophy

Harness 不是技术组件，而是一种**架构设计哲学**（马具思维）。

```
    ┌─────────────┐
    │   专家       │ ←── 导航员（提供方向、校验结果）
    │  (Human)     │
    └──────┬──────┘
           │ 缰绳（控制接口）
           ▼
    ┌─────────────┐
    │  Harness     │ ←── 约束层（控制 Agent 行为）
    │  (Control)   │
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │   Agent      │ ←── 司机（执行分析推理）
    │ (Autonomy)   │
    └─────────────┘
```

**Harness 的三个核心能力：**

1. **方向控制（缰绳）** — 专家告诉 Agent 分析什么
2. **速度控制（刹车）** — 专家控制 Agent 的节奏
3. **行为校正（纠正）** — 专家纠正 Agent 的错误

**Harness 的设计目标：**

> 让 Agent 在可控的前提下发挥最大自主性。

**Agent 的角色定位：**

- Agent 是**主力分析执行者**
- 专家是**导航员**（提供方法论、校验结果、优化流程）
- Harness 是**操作系统**（连接 Agent 和专家的框架）

**专家手动介入：**

当 Agent 推理能力不足时，专家可以直接手动介入，添加 Observation、纠正 Finding 或指定分析方向。

---

## 2. Module Design

### 2.1 Data Layer — 数据采集与管理

**职责：** 管理所有原始数据（Evidence）的采集、存储、传输和检索。

**核心模块：**

| 模块 | 职责 | 关键设计 |
|------|------|---------|
| **Data Collector** | 从手机采集 AP Log / Modem Log / Net Log / 录屏 | 支持 MTK / 高通等平台适配 |
| **Upload Manager** | 将数据上传到服务器 | 断点续传、压缩传输 |
| **Download Manager** | 将数据下载到研发本地 | 按需下载（非全量） |
| **Storage Service** | 数据存储（~10GB/Case） | 冷热数据分层 |
| **Platform Adapter** | 适配不同平台的专用工具 | MTK Log 查看器 / Qualcomm Log 查看器 |

**关键设计决策：**

- 数据传输和分析流程**并行推进**
- 支持**按需下载**（专家标注重点区域后，只下载相关数据）
- 平台适配通过**插件化**方式扩展

### 2.2 Agent Harness — 领域专家 Agent 控制层

**职责：** 控制 Agent 的自主分析行为，提供专家校验点。

**核心模块：**

| 模块 | 职责 | 关键设计 |
|------|------|---------|
| **Agent Controller** | 控制 Agent 的生命周期 | 启动/暂停/恢复/终止 |
| **Direction Setter** | 专家指定 Agent 分析方向 | 指定模块/时间段/对比 Case |
| **Behavior Tuner** | 专家调整 Agent 行为 | 切换 Reasoning Model / 注入 Evidence / 纠正假设 |
| **Result Validator** | 专家校验 Agent 输出 | 通过**结构化输出文档**检查 Evidence → Observation → Finding 链路 |
| **Manual Override** | 专家手动介入分析 | 添加 Observation / 纠正 Finding / 指定分析方向 |
| **Process Logger** | 记录 Agent 分析过程 | 轻量级核心链路追踪 |

**Agent 自主分析流程：**

```
专家定义 Case 问题
    ↓
Agent 自主分析 (高度自主)
    ├─ 读取 Evidence
    ├─ 生成 Observation
    ├─ 提出 Hypothesis
    ├─ 执行 Reasoning
    ├─ 产生 Finding
    └─ 输出结构化分析文档 (核心链路)
    ↓
专家校验 (Result Validator)
    ├─ 审查结构化文档中的证据链
    ├─ 检查 Evidence → Observation → Finding 链路是否合理
    └─ 接受 / 纠正 / 手动介入
    ↓
Agent 根据反馈重新推理 (限于当前 Case)
    ↓
专家最终确认
    ↓
Root Cause → Knowledge Assets
```

**结构化输出文档的内容：**

```
Analysis Report
    ├── Evidence Summary (分析了哪些 Evidence)
    ├── Observations (产生的所有观察)
    ├── Hypotheses (提出的所有假设)
    │   ├── Active (活跃假设)
    │   └── Eliminated (排除的假设 + 原因)
    ├── Findings (推理结论)
    │   └── Supporting Evidence (每个结论的证据链)
    ├── Root Cause (最终结论)
    └── Process Log (Agent 推理过程记录)
```

**专家控制 Agent 的四个维度：**

1. **方向控制** — 指定分析模块、对比 Reference Case、设定分析范围
2. **过程控制** — 暂停/恢复/终止 Agent、要求解释推理步骤
3. **行为调整** — 切换 Reasoning Model、注入新 Evidence、纠正错误假设
4. **结果校验** — 审查结构化输出文档中的证据链

### 2.3 Knowledge Asset Management — 知识资产管理

**职责：** 管理和沉淀 Analysis Case 产生的知识资产。

**核心模块：**

| 模块 | 职责 | 关键设计 |
|------|------|---------|
| **Asset Extractor** | 从 Case 中提取知识资产 | Agent 自动提取 + 专家确认 |
| **Asset Store** | 存储知识资产 | 版本化管理 |
| **Asset Search** | 搜索和检索知识资产 | 按类型/标签/案例 |
| **Asset Updater** | 更新和演进知识资产 | 新 Case 验证后更新 |

**知识资产类型：**

| 类型 | 描述 | 示例 |
|------|------|------|
| **Methodology** | 分析方法论 | 递归缩小法、时间线重建 |
| **Workflow** | 标准工作流程 | 从数据采集到结论确认的完整流程 |
| **SOP** | 标准操作流程 | 现场测试 SOP、Log 分析 SOP |
| **Skills** | AI 可执行的技能 | Agent 可调用的自动化技能 |
| **Evidence Pattern** | 证据模式 | 特定 Evidence 组合指向特定结论 |
| **Root Cause Pattern** | 根因模式 | 已解决的典型案例模式 |
| **Expert Experience** | 专家经验 | 隐性经验显性化 |
| **Reasoning Model** | 推理模型 | 针对特定问题类型的推理策略 |
| **Test Case Template** | 测试用例模板 | 标准化测试用例 |

---

## 3. Data Flow Design

### 3.1 Case Lifecycle Data Flow

```
[1] 测试团队执行测试用例
    ↓ (采集)
[2] AP Log + Modem Log + Net Log + 录屏 + Excel + 背景资料
    ↓ (上传，~10GB)
[3] 服务器存储 (Data Layer)
    ↓ (专家标注重点区域)
[4] 按需下载 (减少传输量)
    ↓
[5] Agent Harness 执行分析 (Agent 自主分析)
    │
    ├── Agent 读取 Evidence
    ├── Agent 生成 Observation / Hypothesis / Finding
    ├── Agent 输出结构化分析文档
    │
    └── 专家校验 (Result Validator)
            ├── 审查结构化文档中的证据链
            ├── 接受 / 纠正 / 手动介入
            └── Agent 根据反馈重新推理 (限于当前 Case)
    ↓
[6] Root Cause 确认
    ↓
[7] Knowledge Asset 提取 (Asset Extractor: Agent 自动提取 + 专家确认)
    ↓
[8] Case 关闭
```

### 3.2 Evidence Flow

Evidence 的生命周期是一个**循环**，不是线性流。

```
[阶段 1] 数据采集 (Investigation)
    测试团队执行测试 → 采集 AP Log + Modem Log + Net Log + 录屏
    ↓
[阶段 2] 数据上传
    数据上传到服务器 (~10GB)
    ↓
[阶段 3] 数据存储
    Storage Service 持久化存储
    ↓
[阶段 4] 数据标注
    测试人员标注重点区域 → 专家知道看什么
    ↓
[阶段 5] 数据分发 (按需下载)
    研发按需下载相关数据 → 减少传输量
    ↓
[阶段 6] 数据消费 (Agent Harness)
    └── Agent 读取 Evidence → 生成结构化分析文档
    ↓
[阶段 7] 专家校验
    └── Result Validator 审查证据链 → 接受/纠正/手动介入
    ↓
[阶段 8] 结果产出
    Observation → Finding → Root Cause
    ↓
[阶段 9] 知识沉淀
    Knowledge Assets 提取 (Agent 自动 + 专家确认)
    ↓
[阶段 10] 如果需要更多数据
    专家提出 Investigation Request → 回到 [阶段 1]
```

**关键设计原则：**

1. **Evidence Store 是 Case 级别的共享存储**，Agent 从中读取 Evidence，但不修改它。
2. **Evidence 是不可变的** — 一旦进入 Evidence Store，不会被修改。新增 Evidence 通过新的 Investigation 产生。
3. **Agent 是唯一的分析执行者** — 所有分析通过 Agent Harness 执行，专家通过结构化文档校验证据链。

---

## 4. Platform Adaptation Design

### 4.1 Platform Adapter Plugin Architecture

```
┌─────────────────────────────────────────────┐
│           Platform Adapter Layer             │
├─────────────────────────────────────────────┤
│  MTK Adapter │ Qualcomm Adapter │ Others... │
├─────────────────────────────────────────────┤
│        Common Log Parser Interface          │
├─────────────────────────────────────────────┤
│  AP Log │ Modem Log │ Net Log │ Others     │
└─────────────────────────────────────────────┘
```

**设计原则：**

- 每种平台的专用工具通过**插件**方式接入
- 插件实现统一的 Log Parser Interface
- 新增平台只需开发新插件，不影响核心引擎

---

## 5. Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-031 | 数据传输和分析流程并行推进 | Frozen |
| D-032 | Agent 高度自主，专家在关键节点校验 | Frozen |
| D-033 | Agent 学习限于当前 Case，不跨 Case 复用 | Frozen |
| D-034 | Agent 过程数据只需核心链路追踪 | Frozen |
| D-035 | 平台适配通过插件化方式扩展 | Frozen |
| D-036 | 支持按需下载以减少传输量 | Frozen |
| D-037 | Agent 是唯一的分析执行者 | Frozen |
| D-038 | Knowledge Asset 提取采用 Agent 自动提取 + 专家确认 | Frozen |
| D-039 | 专家通过结构化输出文档校验 Agent 的证据链 | Frozen |
| D-040 | Harness 是架构设计哲学（马具思维），不是技术组件 | Frozen |
| D-041 | 专家可随时手动介入分析（添加 Observation / 纠正 Finding） | Frozen |

---

## 6. Cross-References

- **FP-001** CEAP Definition — 四层架构实现 Platform Layer
- **VS-001** Vision Statement — 架构设计支持 Vision 的四大目标
- **VF-001** Value Framework — 各模块映射到价值层级
- **BS-001** Current State — 架构回应六大挑战
- **AP-001** Architecture Principles — 架构设计符合 13 条原则
- **CM-002** Core Concept Model — 模块设计基于核心概念
- **CM-003** Ubiquitous Language — Agent, Harness, Team defined in CM-003
- **B-001** Investigation & Classification — 模块职责分离
- **ADR-001** Analysis Case — Case 管理模块实现
- **ADR-002** Reasoning Framework — Agent Harness 集成推理模型
- **ADR-003** Evidence-Driven Analysis — Evidence 存储和管理
- **WF-001** Architecture Workflow — 架构设计遵循此工作流
