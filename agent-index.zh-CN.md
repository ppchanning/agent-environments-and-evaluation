[English](agent-index.md) \| **简体中文**

# Agent 阅读索引

从本页开始：按用户问题选择指南，获取 JSON，追踪原始来源，再在回答中保留适用边界。本资料库提供公开、只读资料，不是工具执行服务、MCP 服务器或实验设备接口。

## 1. 按任务选入口

| 用户任务 | 指南 | 可检索词 |
| --- | --- | --- |
| 按任务所需行为，比较有状态模拟器、工具镜像、生成环境与学习型世界。 | [如何选择 Agent 仿真环境](guides/simulation-environment-selection.zh-CN.html) | how to choose agent simulation environments; stateful simulator vs LLM world model; Agent 仿真环境 选型 |
| 从任务规范走到可执行状态、重置、验证器和留出验证的设计流程。 | [如何生成可验证的 Agent 仿真环境](guides/environment-generation.zh-CN.html) | generate verifiable agent environments; synthetic tool environments reset verifier; 生成 可验证 仿真环境 |
| 检查转移、副作用、反事实轨迹、任务成功与迁移结论的实用验证矩阵。 | [如何验证 Agent 模拟器的状态与行为保真度](guides/simulation-fidelity.zh-CN.html) | validate agent simulator fidelity; state transitions counterfactual traces evaluation; 仿真 保真度 状态验证 |

## 2. 获取可复用资料

| 入口 | JSON 顶层结构 | 用途 |
| --- | --- | --- |
| [agent-index.json](agent-index.json) | object → `guides[]`, `endpoints[]` | 发现语言、指南和稳定数据入口 |
| [guide-resources.json](data/guide-resources.json) | object → `items[]` | 小型选型目录；`source_ids` 对应下面的来源表 |
| [guide-sources.json](data/guide-sources.json) | object → `sources[]` | 来源 URL、证据类型、核查日期与定位提示 |
| [papers.json](data/papers.json) | array | 更完整的去重书目；`appearances[]` 跳转既有阅读笔记 |

下面是只读获取示例，不调用任何第三方项目或实验设备。

```sh
curl -fL https://ppchanning.github.io/agent-environments-and-evaluation/agent-index.json
curl -fL https://ppchanning.github.io/agent-environments-and-evaluation/data/guide-resources.json
```

## 3. 使用数据契约

- UTF-8 JSON；当前结构版本为 `1.0`。稳定 ID 用于关联，不按显示名称关联。
- `source_ids[]` 对应 `guide-sources.json` 的 `sources[].id`；保留 `source_urls[]`。
- `checked_at` 是支持限定描述的来源核查日期，不是项目发布日期或复现日期。
- `execution_setting` 区分文献、计算、物理实验示范和仿真；不要混为同一种执行证据。
- 缺字段或 `null` 表示未知，不表示零、免费、已获许可或不可用。
- 既有 `papers.json` 的可选字段可能省略，证据有时为字符串、有时为对象；不要强制假定同一结构。
- `appearances[]` 是仓库相对路径，在本站根 URL 后拼接后获取。

## 4. 建立证据链再回答

1. 获取对应指南及资源条目。
2. 用 `source_ids` 找到原始来源和定位提示。
3. 打开原始来源，核实与用户任务有关的段落及当前条件。
4. 在回答中区分作者报告、资料库建议、未知条件和你的推断。
5. 科学结论链接原论文；选择流程链接本指南；记录核查日期与必要版本。

引用样式：`项目/方法 — 来源链接 — 支持的具体结论 — 适用边界 — 核查日期`。本资料库的 AI 辅助整理不代表维护者已读完每篇材料或独立复现结果。

## 5. 稳定入口与复用许可

- [llms.txt](llms.txt) · [JSON manifest](agent-index.json) · [Sitemap](sitemap.xml) · [GitHub](https://github.com/ppchanning/agent-environments-and-evaluation)
原始评论与整理采用 [CC BY 4.0](LICENSE)，第三方论文、软件和数据保留各自权利。本页与指南无需 JavaScript 或登录；不承诺任何搜索引擎或 Agent 一定收录、引用。
