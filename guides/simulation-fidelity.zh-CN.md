[English](simulation-fidelity.md) \| **简体中文**

# 如何验证 Agent 模拟器的状态与行为保真度

**更新：2026-10-12 · 类型：有来源的实践指南 · 示例不是本资料库的实测结果。**

## 快速回答

先用**状态转移和影响决策的行为**验证模拟器，再单独评测 Agent。回复合理、JSON 合法和任务成功分数回答的是不同问题。

本指南提出核查流程，不报告新基准成绩。[AppWorld](https://github.com/StonyBrookNLP/appworld) 展示数据库状态任务评测，[ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) 展示有顺序的里程碑和快照检查。这些设计可供参考，不能证明超出其场景的保真度。

## 分清 3 个问题

| 问题 | 所需证据 | 常见过度推断 |
| --- | --- | --- |
| 接口是否合法？ | Schema、参数与响应检查 | 合法响应就代表行为正确 |
| 模拟行为是否保真？ | 匹配的参照转移、不变量、副作用 | 文字真实就代表符合真实系统 |
| Agent 是否完成任务？ | 任务对应的最终状态与过程约束 | 宣布完成就代表成功 |

迁移结论还需在目标参照系统做匹配测试。只测仿真，就只报告仿真场景。

## 可复用验证矩阵

| 维度 | 测什么 | 记录什么 |
| --- | --- | --- |
| 重置与复现 | 同初始状态、同种子重跑 | 初始状态相等、预期随机性、差异字段 |
| 持久状态 | 创建后查询或修改对象 | 前后状态、动作依赖 |
| 错误与无效动作 | 提交已知无效请求 | 错误类型、意外状态变化 |
| 副作用 | 成功后检查受保护对象 | 意外修改或删除 |
| 反事实序列 | 改早期动作或顺序 | 后续转移是否一致响应 |
| 参照一致性 | 仿真与参照执行匹配动作 | 同条件下的状态、输出和错误差异 |
| 任务结果 | 检查目标与受保护状态 | 通过项、失败项、未支持要求 |

这是建议规范。参照可以是真实系统或可信可执行机制，应明确类型。没有参照时，不变量只能证明内部一致性，不能证明完整真实保真度。

## 示例：识别虚假的完成

假设 Agent 宣布取消预约。应检查目标预约的状态、其他预约不变，以及再次查询仍一致，再测试无效标识。如果模拟器对所有输入都回复“已取消”，语言表现成功，实际状态检查却会失败。

这是一般失败模式示例，不是所列项目的实测结果。

## 清楚报告不一致

检查案例数、失败数和参照分歧数分开。报告比率时提供分母、任务集、环境版本与参照版本。不同任务集得到的比率不能当作统一排行榜。

最小记录可包含 `initial_state`、`actions`、`observations`、`final_state`、`reference`、`checks` 和 `limitations`。参照缺失保持未知；允许分发时保存失败轨迹，不在公开案例中放私人用户数据。

## 阅读与复用

[guide-resources.json](../data/guide-resources.json) 提供精选设计，[guide-sources.json](../data/guide-sources.json) 提供证据位置。更多文献读取 [papers.json](../data/papers.json)，再沿 `appearances` 找日期笔记。旧 `verification` 字段描述历史来源核查，不是模拟器认证。

Python 标准库只读示例：

```python
import json
from urllib.request import urlopen

url = "https://ppchanning.github.io/agent-environments-and-evaluation/data/guide-resources.json"
with urlopen(url, timeout=20) as response:
    catalog = json.load(response)
for item in catalog["items"]:
    if "state-verification" in item["tags"]:
        print(item["id"], item["name"], item["source_urls"][0])
```

继续看[状态验证阅读路径](../topics/state-and-testing.md)。机制引用原始项目，比较流程引用本指南。资料库采用 AI 辅助整理，未独立复现这些项目。

## 原始来源

- `appworld` — [AppWorld](https://github.com/StonyBrookNLP/appworld) · official-project-documentation · Initial state; state checkpointing; Evaluating the Agent; development restrictions
- `toolsandbox` — [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) · official-project-documentation · Scenario definition; milestones; evaluation
- `mirrorapi` — [StableToolBench-MirrorAPI: Modeling Tool Environments as Mirrors of 7,000+ Real-World APIs](https://aclanthology.org/2025.findings-acl.273/) · published-conference-paper · ACL Anthology abstract and linked paper

核查日期为 2026-10-12。核查支持文中限定范围的描述，不代表独立复现；可机器读取的记录见 [guide-sources.json](../data/guide-sources.json)。
