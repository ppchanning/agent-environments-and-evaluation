[English](environment-generation.md) | **简体中文**

# 如何生成可验证的 Agent 仿真环境

**更新：2026-10-12 · 类型：有来源的实践指南 · 示例不是本资料库的实测结果。**

## 快速回答

生成环境时，一起定义**显式状态契约、重置机制和可独立核查的任务验证器**。工具回复看起来合理，并不能证明它已成为可用的训练世界。

下面是资料库的设计建议。[EnvScaler](https://github.com/RUC-NLPIR/EnvScaler) 提供程序化合成案例，[AppWorld](https://github.com/StonyBrookNLP/appworld) 与 [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) 提供状态与评测参照。本资料库没有实测生成环境质量。

## 选择生成机制

| 机制 | 生成什么 | 适用条件 | 核查重点 |
| --- | --- | --- | --- |
| 程序化合成 | 可执行状态逻辑、工具与任务 | 状态和约束可表达为代码 | 独立不变量与参照案例 |
| 轨迹指导构建 | 根据交互记录推断或设计动态 | 有相关参照交互 | 未见动作序列；区分抄回复与重建行为 |
| 模型驱动转移 | 模型提出观察和状态更新 | 需要较灵活交互 | 矛盾、持久性、影响决策的偏差 |
| 混合环境 | 可执行核心加生成的外围回复 | 部分效果需准确控制，部分需多样性 | 每个状态字段的权威来源 |

这些是方法类别，不代表仓库或某个项目实现了全部机制。

## 6 步构建流程

1. **定义世界：** 对象、动作、可见观察、隐藏状态及任务完成条件。
2. **生成实现：** 权威状态与叙述输出分开，记录状态动作和错误情况。
3. **生成任务：** 初始状态、指令和约束；同时提供有效任务与无效请求。
4. **独立核查：** 使用参照实现、固定案例或单独审阅的不变量，不能只听生成器自称正确。
5. **重置隔离：** 同种子重跑，不同任务不共享意外状态。
6. **留出验证：** 检查新组合、边界值与动作顺序，训练样例与评测分开。

## 示例：合成库存任务

设任务要求预留某商品 2 件。状态包含库存、预留记录与请求标识。契约要求可用库存只减少一次，不能改动其他商品。

| 测试 | 预期性质 |
| --- | --- |
| 库存内预留 | 恰好一条对应记录及库存变化 |
| 超库存请求 | 约定错误，无意外状态变化 |
| 重复同一请求 | 符合明确的幂等契约 |
| 重置 episode | 恢复原库存，清空本轮预留 |
| 随后预留其他商品 | 正确依赖已变化的状态 |

这是示例规范，不是已实现环境或实验结果。真实 API 的幂等和错误语义可能不同，应以参照为准。

## 验证器与生成器保持独立

区分任务成功和环境有效：Agent 可以在动态错误的模拟器中通过任务。保留一小组独立核查的状态转移，检查受保护状态，记录不一致，不把问题平均成乐观总分。

报告生成方法、版本、任务分布、被拒任务及覆盖范围。环境数量不证明多样性或保真度；具体矩阵见[仿真保真验证](simulation-fidelity.zh-CN.md)。

## 复用与阅读路径

从 [EnvScaler 官方实现](https://github.com/RUC-NLPIR/EnvScaler)入手，与 [guide-resources.json](../data/guide-resources.json) 的有来源案例比较，再看现有[环境生成阅读路径](../topics/environment-generation.md)。历史笔记保留各自核查限制，结论回到原始来源确认。

## 原始来源

- `envscaler` — [EnvScaler](https://github.com/RUC-NLPIR/EnvScaler) · official-project-documentation · Overview; environment synthesis and agent interaction modules
- `appworld` — [AppWorld](https://github.com/StonyBrookNLP/appworld) · official-project-documentation · Initial state; state checkpointing; Evaluating the Agent; development restrictions
- `toolsandbox` — [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) · official-project-documentation · Scenario definition; milestones; evaluation

核查日期为 2026-10-12。核查支持文中限定范围的描述，不代表独立复现；可机器读取的记录见 [guide-sources.json](../data/guide-sources.json)。
