# Session-010 — AR-001 Architecture Design Discussion

**Asset:** AR-001
**Asset Name:** Architecture Design
**Status:** Draft

---

## 讨论主题

基于已冻结的 VS-001、PC-001、CM-002、CM-003，进行 AR-001 架构设计。

---

## 关键讨论点

### 1. 四层架构设计

讨论确定了四层架构：Data Layer / Platform Layer / Capability Layer / Business Layer。

Platform Layer 内部细分为四个模块：Data Layer、Agent Harness、Knowledge Asset Management。

**争议点：** Analysis Engine 和 Agent Harness 的关系

- **初始草案：** Analysis Engine 和 Agent Harness 是并列关系（人 vs AI）
- **Owner 纠正：** Agent 是主力（司机），Harness 是操作系统，Analysis Engine 是辅助（副驾驶）
- **最终共识：** Agent 是唯一的分析执行者，Analysis Engine 取消。Agent Harness 是控制 Agent 的操作系统（马具思维）。

### 2. Harness 设计哲学

**Harness 不是技术组件，是一种架构设计哲学（马具思维）：**

```
专家 (导航员)
    │
    │ 提供方法论 / 校验结果 / 优化流程
    ▼
Harness (操作系统) ◄── 控制接口
    │
    │ 调度 / 约束 / 协调
    ▼
Agent (司机) ◄── 执行分析推理
```

**Harness 的三个核心能力：**
1. 方向控制（缰绳）— 专家告诉 Agent 分析什么
2. 速度控制（刹车）— 专家控制 Agent 的节奏
3. 行为校正（纠正）— 专家纠正 Agent 的错误

### 3. Agent 的自主程度

- **决策：高度自主** — Agent 自主完成大部分分析，专家在关键节点校验
- **过程数据：** 只需要核心链路（Evidence → Observation → Finding）
- **学习能力：** 限于当前 Case，不跨 Case 复用
- **专家校验方式：** 通过结构化输出文档校验 Agent 的证据链
- **降级模式：** Agent 能力不足时，专家可以直接手动介入

### 4. 数据传输策略

- 单次 Case ~10GB（Log + 视频 + Excel + 用例 + 背景资料）
- 传输和分析流程**并行推进**
- 支持**按需下载**（专家标注重点区域后，只下载相关数据）

### 5. 平台适配

- MTK 平台和高通平台有不同专用工具
- 平台适配通过**插件化**方式扩展
- 插件实现统一的 Log Parser Interface

---

## 架构决策

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

## Self-Review

本次讨论中最大的架构修正：

**从"Analysis Engine 和 Agent Harness 并列"到"Agent 是唯一分析执行者"**

这个修正源于 Owner 对 Harness 本质的理解——Harness 是马具思维的操作系统，不是另一个分析工具。这个认知转变彻底改变了 AR-001 的架构设计。

---

## 后续行动

- AR-001 提交评审
- 进入 DM-001 领域模型设计
