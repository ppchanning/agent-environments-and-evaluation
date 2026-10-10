<p align="center"><img src="assets/banner.svg" alt="Agent Environments &amp; Evaluation" width="100%"></p>

<h1 align="center">Agent Environments &amp; Evaluation</h1>
<p align="center"><strong>Agent 环境、仿真与评测的论文及技术阅读地图</strong><br>Explore the tools, executable worlds, and evidence behind reliable AI agents.</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/content-CC_BY_4.0-6366f1" alt="Content license: CC BY 4.0"></a>
  <a href="topics/README.md"><img src="https://img.shields.io/badge/focus-tools_%7C_simulation_%7C_evaluation-0284c7" alt="Tools, simulation and evaluation"></a>
  <a href="CONTRIBUTING.md"><img src="https://img.shields.io/badge/notes-中文_%2B_English-334155" alt="Chinese notes and English paper titles"></a>
</p>

<p align="center"><a href="#start-here">快速开始</a> · <a href="#explore-the-landscape">主题地图</a> · <a href="#selected-reading">代表资料</a> · <a href="resources/papers.md">完整书目</a> · <a href="digests/README.md">晨读归档</a> · <a href="CONTRIBUTING.md">参与贡献</a></p>

**理解 Agent 如何与外部世界交互，以及怎样判断它真正完成了任务。**

一个 Agent 的表现与它可用的工具、能够观察的状态、执行动作的环境以及成功标准密切相关。本仓库围绕这些系统环节整理论文与技术案例：从 MCP / API 工具接口，到有状态的软件模拟器、自动生成的训练环境、长任务轨迹与行为评测。

你可以在这里发现值得读的工作，比较环境与评测设计，寻找构建测试环境的思路，并追溯“任务完成”这一结论由什么证据支持。阅读笔记将论文的问题、方法、证据、限制和建议阅读章节放在一起，便于从标题走向原文。

## Start here

| 你想解决什么问题 | 阅读入口 | 可以获得什么 |
| --- | --- | --- |
| 最近有哪些值得关注的论文？ | [最新晨读](digests/agent-environments/2026/2026-10-10.md) · [历史归档](digests/README.md) | 每期推荐、方法解读、证据限制和原始来源 |
| Agent 的工具接口应该怎样理解和测试？ | [工具协议与 API](topics/tool-protocols.md) | 接口描述、工具调用与实际行为之间的研究线索 |
| 如何为 Agent 构建可交互、可校验的环境？ | [环境生成与仿真](topics/environment-generation.md) | 自动生成环境、轨迹驱动模拟与世界模型相关方法 |
| 怎样检查动作是否真的改变了系统？ | [状态与行为测试](topics/state-and-testing.md) | 状态转移、隐藏状态、行为一致性与验证问题 |
| 怎样衡量长任务和真实完成情况？ | [Agent 评测](topics/agent-evaluation.md) | 过程评测、执行轨迹、任务结果与环境偏差的阅读路径 |
| 如何整理自己的相关工作表？ | [完整书目](resources/papers.md) · [JSON 数据](data/README.md) | 去重标识、来源、版本与出现记录，便于筛选和继续阅读 |

适合 Agent 系统开发者、工具与 MCP 服务开发者、环境及评测研究者，也适合希望从通用 Agent 论文进入具体系统问题的学生。中文笔记保留英文题名与原始出处。

## Explore the landscape

### Tools, protocols & APIs · 工具接口与协议

工具 schema 描述输入输出，执行系统决定真实行为。该主题关注工具使用、MCP / API 交互及接口与行为之间的关系，帮助读者为调用成功、参数有效和任务完成建立不同层面的判断。

**阅读入口：** [Tool protocols & APIs](topics/tool-protocols.md)

### Environment generation & simulation · 环境生成与仿真

Agent 的训练与测试需要可交互的任务世界。该主题连接自动生成环境、轨迹驱动模拟、语言世界模型和可验证机制，关注环境从哪里来、能保持哪些行为、怎样提供反馈，以及模拟与真实系统有哪些差距。

**阅读入口：** [Environment generation](topics/environment-generation.md)

### State & behavioral verification · 状态与行为验证

返回成功、数据库发生变化和用户目标达成，是不同的证据。该主题关注持久状态、动作序列、隐藏动态和行为一致性，提供理解有状态模拟器及检查任务结果的阅读线索。

**阅读入口：** [State & behavioral testing](topics/state-and-testing.md)

### Agent evaluation & execution evidence · 评测与执行证据

面对长任务，最终分数往往需要结合执行过程理解。该主题关注轨迹、过程指标、结果验证、可观测性与环境变化，帮助读者比较论文各自测量了什么，避免脱离任务和环境解释成绩。

**阅读入口：** [Agent evaluation](topics/agent-evaluation.md)

## Selected reading

下面按阅读问题展示代表资料。题目链接指向原始来源，中文问题是本集合的阅读切入点；完整元数据与关联晨读见 [Paper Catalog](resources/papers.md)。

| 阅读问题 | 代表资料 | 关联主题 |
| --- | --- | --- |
| 交互轨迹如何变成可执行的模拟世界？ | [From Traces to Agentic Worlds](https://arxiv.org/abs/2610.06100) | 环境生成、世界模型 |
| 如何自动生成带验证机制的技能训练环境？ | [SkillGym](https://arxiv.org/abs/2609.37539) | 环境生成、工具使用 |
| 有状态的软件模拟器怎样接受行为检查？ | [CTE-Bench](https://arxiv.org/abs/2609.36647) | 仿真、状态、评测 |
| Agent 宣称完成后，应该检查什么系统证据？ | [The Agent Said It Was Done. The Database Disagreed.](https://huggingface.co/blog/microsoft/thinkingbox) | 任务验证、真实状态 |
| Computer-use 任务的执行过程如何评价？ | [OSWorld-Pro](https://arxiv.org/abs/2609.24890) | 执行轨迹、过程评测 |

## What a reading note gives you

每期围绕以下问题组织内容，具体深度取决于可访问的原始证据：

- **问题与场景：** 研究针对哪类 Agent、工具或任务，为什么需要这个环境或评测。
- **方法与系统：** 环境如何运行，Agent 能观察和执行什么，关键机制在哪里。
- **作者证据：** 使用哪些数据、任务和对照，结果支持什么范围的结论。
- **限制与迁移条件：** 模拟与真实执行的差距、未覆盖的行为，以及理解结果需要保留的条件。
- **继续阅读：** 原论文链接、版本信息及适合优先阅读的章节。

主题目录支持横向比较，日期归档支持持续跟踪，结构化书目支持本地检索。它们共同帮助读者建立自己的相关工作和方法地图。

## Collection at a glance

<!-- collection-stats:start -->
截至 **2026-10-10**：**11 期晨读 · 43 项去重资料 · 4 条专题阅读路径**。

晨读归档覆盖 2026-09-28 至 2026-10-10，日期范围内可能有缺期。新增与修订材料按日期归档，最新入口、主题索引和去重书目一起维护。
<!-- collection-stats:end -->

## How to use this repository

1. **首次进入：** 选一个实际问题，从对应主题页挑选论文，再结合晨读找到阅读重点。
2. **持续跟踪：** 阅读最新一期，通过历史归档回看同一方向的方法变化。
3. **设计系统或评测：** 比较不同工作中的状态、动作、反馈和验证机制；回到原文确认适用条件。
4. **整理相关工作：** 下载 [papers.json](data/papers.json)，按标识、版本和出现记录去重，建立自己的文献表。可选字段可能缺失，详见 [Data Guide](data/README.md)。
5. **贡献资料：** 推荐有来源的论文或技术案例，改进主题归类和元数据，或提交证据纠错。见 [贡献指南](CONTRIBUTING.md) 与 [Issues](https://github.com/ppchanning/agent-environments-and-evaluation/issues)。

## Repository map

```text
digests/       # 论文晨读：频道 / 年份 / 日期
topics/        # 工具、环境生成、状态行为与评测
resources/     # 完整书目与原始来源入口
data/          # 去重 JSON 书目与字段说明
docs/          # 编辑标准、分享说明与设计参考
templates/     # 新增资料的统一模板
.github/       # 推荐资料、纠错与 Pull Request 模板
```

## Sources, contributions & citation

这是论文与技术资料集合，提供阅读和比较系统设计所需的材料。可执行环境、基准实现或评测结果以各原始项目为准。整理区分预印本、正式论文及官方案例，保留来源、版本和证据限制；内容由 AI 辅助整理，不推断维护者已读完或独立复现。详见 [Editorial Policy](docs/editorial-policy.md)。

欢迎补充论文、技术案例、阅读路径与纠错，见 [CONTRIBUTING](CONTRIBUTING.md)。原创说明与汇编采用 [CC BY 4.0](LICENSE)，第三方作品保留各自权利。科研结论请引用原论文；引用本集合可使用 [CITATION.cff](CITATION.cff)。

**Related collection:** [AI4Science Observatory](https://github.com/ppchanning/ai4science-observatory) 聚焦 AI 科学发现、科研智能体、科学软件和远程真实实验。

[分享说明](docs/sharing.md) · [设计参考](docs/design-references.md)
