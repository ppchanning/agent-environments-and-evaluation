[English](simulation-environment-selection.md) \| **简体中文**

# 如何选择 Agent 仿真环境

**更新：2026-10-12 · 类型：有来源的实践指南 · 示例不是本资料库的实测结果。**

## 快速回答

按**一串动作之后，哪些状态与行为必须仍然正确**来选择 Agent 仿真环境。若数据库变化决定任务成功，优先检查显式状态与可执行验证；若需要丰富交互，可考虑生成式或模型驱动世界，但其转移仍需独立参照。

本指南提供设计与阅读地图。仓库不提供这些模拟器的实现，也不认证真实世界保真度。以下原始文档于 2026-10-12 核查，未独立运行。

## 比较 4 个入口

| 入口 | 环境方式 | 阅读价值 | 需要保留的边界 |
| --- | --- | --- | --- |
| [AppWorld](https://github.com/StonyBrookNLP/appworld) | 有底层状态的可控应用世界 | 任务、数据库状态、检查点和任务评测 | 应用仿真不是操作真实用户账户；检查点权限影响公平比较 |
| [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) | 有状态工具交互，配场景与里程碑评测 | 持久状态和交互顺序要求 | 给定场景的检查不能证明任意外部服务保真 |
| [EnvScaler](https://github.com/RUC-NLPIR/EnvScaler) | 程序化合成可执行、有状态的工具环境 | 环境生成与交互的连接 | 生成后能执行，不等于符合真实服务行为 |
| [StableToolBench-MirrorAPI](https://aclanthology.org/2025.findings-acl.273/) | 以真实 API 行为为参照的工具镜像 | 工具服务仿真的设计 | 迁移结论前先读构建与评测条件 |

此表比较方案，不比较统一性能。工具协议描述接口，模拟器还需定义接口背后的状态转移。

## 按任务选择

| 任务要求 | 优先检查 | 决定性核查 |
| --- | --- | --- |
| 创建、修改、删除对象 | 显式有状态模拟器 | 最终状态和所有受保护对象是否正确？ |
| 有依赖的长动作序列 | 持久状态与轨迹检查 | 前面的动作是否改变后续前提和观察？ |
| 大量新工具场景 | 程序化环境生成 | 任务是否可解、多样并可独立验证？ |
| 灵活文本世界 | 学习型或语言模型转移 | 参照轨迹和反事实动作能否暴露动态不一致？ |
| 迁移到真实系统 | 参照系统与匹配测试 | 哪些动作仿真成功，却在真实接口或约束下失败？ |

最后两行是选型启发，不表示某个列出的项目已通过这些检查。

## 最小环境契约

选择前写清：

- **状态：** 持久对象、隐藏变量和 episode 之间的归属。
- **动作：** 工具参数、单位、前提与副作用。
- **观察：** Agent 看见什么，包括错误和延迟。
- **重置：** 恢复哪些状态，还有哪些随机性。
- **验证：** 如何检查任务完成及意外改动。
- **参照：** 真实系统、形式机制或可信可执行规范；没有则说明。

例如日历任务可要求新增一个字段正确的事件，同时其他事件不变。这是一般示例，不是实测基准成绩。

## 如何输出有用的推荐

推荐应列出目标任务、环境类型、状态要求、候选来源、验证缺口及权限或许可条件。没有参照系统，就说明保真度尚未建立，不编造数字信任评分。

继续读[环境生成](environment-generation.zh-CN.md)和[仿真保真验证](simulation-fidelity.zh-CN.md)。机器读取使用 [agent-index.json](../agent-index.json) 和 [guide-resources.json](../data/guide-resources.json)，[papers.json](../data/papers.json) 保留较广的历史阅读记录。

## 原始来源

- `appworld` — [AppWorld](https://github.com/StonyBrookNLP/appworld) · official-project-documentation · Initial state; state checkpointing; Evaluating the Agent; development restrictions
- `toolsandbox` — [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) · official-project-documentation · Scenario definition; milestones; evaluation
- `envscaler` — [EnvScaler](https://github.com/RUC-NLPIR/EnvScaler) · official-project-documentation · Overview; environment synthesis and agent interaction modules
- `mirrorapi` — [StableToolBench-MirrorAPI: Modeling Tool Environments as Mirrors of 7,000+ Real-World APIs](https://aclanthology.org/2025.findings-acl.273/) · published-conference-paper · ACL Anthology abstract and linked paper

核查日期为 2026-10-12。核查支持文中限定范围的描述，不代表独立复现；可机器读取的记录见 [guide-sources.json](../data/guide-sources.json)。
