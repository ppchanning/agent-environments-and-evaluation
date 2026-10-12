# Data Guide

[papers.json](papers.json) 为去重书目。字段：id/title/DOI/arXiv/URL/作者/首发与版本/evidence/limitations/read_first/appearances[]/provenance。appearances 为相对归档路径；可选字段未知时省略，证据可能为字符串或对象。标识优先去版本 arXiv ID、DOI、规范 URL。

历史核验来自上游 AI 辅助资料，不推断维护者实读状态。

## Core-guide data (schema 1.0)

| 文件 | 顶层结构 | 内容 |
| --- | --- | --- |
| [guide-resources.json](guide-resources.json) | object → `items[]` | 核心指南的小型案例目录；与既有完整书目分开计数 |
| [guide-sources.json](guide-sources.json) | object → `sources[]` | 原始来源、证据类型、核查日期和定位提示 |
| [../agent-index.json](../agent-index.json) | object → `guides[]`, `endpoints[]` | 指南、语言、任务别名与公开数据入口 |

用 `source_ids[]` 关联 `sources[].id`。`checked_at` 只表示支持限定描述的来源核查；`independently_reproduced: false` 明确未独立复现。`execution_setting` 区分文献、计算、物理实验与仿真。缺字段或 null 仍表示未知。

完整英文与中文读取、引用流程见 [Agent index](../agent-index.md) / [Agent 索引](../agent-index.zh-CN.md)。原始评论和整理采用 CC BY 4.0，第三方材料权利不变。
