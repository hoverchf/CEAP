# Session-011 — DM-001 Domain Model Discussion

**Asset:** DM-001
**Asset Name:** Domain Model
**Status:** Draft

---

## 讨论主题

基于已冻结的 CM-002、CM-003、AR-001，进行 DM-001 领域模型设计。

---

## 关键讨论点

### 1. Session 的角色

**初始草案：** 将 Session 标记为"已取消，Agent 是唯一的分析执行者"

**Owner 纠正：** Session 没有被取消。Session 是 Case 内的一次分析活动，Agent 是 Session 的执行主体。Session 作为"分析活动"的概念仍然存在。

**最终共识：**
- Session 是系统操作的最小实体
- Team 是公司管理组织方式
- Session 是团队间传递分析结果的载体

### 2. Root Cause Evidence Chain

**新增：** Root Cause 必须有完整的证据链。

从 Root Cause 回溯到所有支撑 Evidence 的完整链路，每个节点包含 Evidence/Observation/Hypothesis/Finding，并带有置信度。

### 3. 多团队协作模型

**初始草案：** 多团队并行分析

**Owner 纠正：** 团队间既有并行也有串行：
- 并行：各团队同时分析各自模块
- 串行：一个 Session 的输出触发另一个团队的 Session
- 共享：所有团队共享同一个 Case 的 Evidence Store
- 传递：团队间的传递通过 Session 的输出实现

### 4. Problem Type vs Problem Family

**初始草案：** 命名为 Problem Type，定位为 Case 的分类标签

**Owner 纠正：** 如果它只是分类标签，作为 Case 的一个字段就够了。但如果它要作为多个 Case 的载体（共享分析方法论和知识资产），那它不是一个"类型"，而是一个"问题家族"。

**最终共识：**
- 更名为 **Problem Family**
- 包含共享的分析方法论（持续演进）
- 包含共享的知识资产
- 一个 Case 属于一个 Problem Family
- Case 可以在不同 Problem Family 之间调整

### 5. Team 和 Session 的关系

- 一个团队可以有多个 Session
- 一个 Session 只属于一个团队
- Session 是系统操作的最小实体，Team 是管理组织方式

---

## 架构决策

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

## Self-Review

本次讨论中最重要的架构修正：

**1. Session 没有被取消** — 这是对 AR-001 中错误的纠正。Session 是 Case 内的一次分析活动，Agent 只是执行主体。

**2. Problem Type → Problem Family** — 从分类标签升级为问题家族，包含共享方法论和知识资产。

**3. 团队关系修正** — 从纯并行改为并行+串行，Session 是传递载体。

这三个修正都影响了 DM-001 的领域模型设计，但**不影响已冻结的资产**（CM-002、CM-003、AR-001 都还未冻结）。

---

## 后续行动

- DM-001 提交评审
- 检查已冻结资产是否需要更新
