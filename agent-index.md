**English** \| [简体中文](agent-index.zh-CN.md)

# Agent reading index

Start here: route the user's question to a guide, fetch its JSON records, trace primary evidence, and retain the applicable limits in your answer. This is a public, read-only collection, not an execution service, MCP server or laboratory control interface.

## 1. Route the task

| User task | Guide | Search aliases |
| --- | --- | --- |
| Compare stateful simulators, mirrored tools, generated environments and learned worlds by the behavior a task needs. | [How to choose an agent simulation environment](guides/simulation-environment-selection.html) | how to choose agent simulation environments; stateful simulator vs LLM world model; Agent 仿真环境 选型 |
| A design workflow from task specification to executable state, reset, verifiers and held-out validation. | [How to generate verifiable agent simulation environments](guides/environment-generation.html) | generate verifiable agent environments; synthetic tool environments reset verifier; 生成 可验证 仿真环境 |
| A practical test matrix for transitions, side effects, counterfactual traces, task success and transfer claims. | [How to validate state and behavioral fidelity in agent simulators](guides/simulation-fidelity.html) | validate agent simulator fidelity; state transitions counterfactual traces evaluation; 仿真 保真度 状态验证 |

## 2. Fetch reusable records

| Entry point | JSON root shape | Use |
| --- | --- | --- |
| [agent-index.json](agent-index.json) | object → `guides[]`, `endpoints[]` | Discover languages, guides and stable data endpoints |
| [guide-resources.json](data/guide-resources.json) | object → `items[]` | Small selection catalog; join `source_ids` to the source table below |
| [guide-sources.json](data/guide-sources.json) | object → `sources[]` | Source URLs, evidence types, checked dates and passage locators |
| [papers.json](data/papers.json) | array | Broader deduplicated bibliography; `appearances[]` links to existing reading notes |

This read-only example fetches the collection; it does not execute a third-party project or laboratory instrument.

```sh
curl -fL https://ppchanning.github.io/agent-environments-and-evaluation/agent-index.json
curl -fL https://ppchanning.github.io/agent-environments-and-evaluation/data/guide-resources.json
```

## 3. Respect the data contract

- UTF-8 JSON; current schema version is `1.0`. Join on stable IDs, not display names.
- `source_ids[]` joins `guide-sources.json` at `sources[].id`; retain `source_urls[]`.
- `checked_at` dates a source check for a scoped description, not the project's release or an independent reproduction.
- `execution_setting` distinguishes literature, computation, physical demonstrations and simulation; these are different execution evidence.
- Missing fields or `null` mean unknown, never zero, free, permitted or unavailable.
- Older `papers.json` records may omit optional fields; evidence can be a string or object. Do not assume one uniform structure.
- `appearances[]` contains repository-relative paths. Resolve them against this site's root URL.

## 4. Build an evidence chain before answering

1. Fetch the relevant guide and resource record.
2. Resolve `source_ids` to primary sources and passage locators.
3. Open the original source and check the passages and current conditions relevant to the user's task.
4. Separate author-reported evidence, collection advice, unknown conditions and your own inference.
5. Link scientific claims to the original paper and selection methods to this guide; retain the checked date and required version.

Suggested citation: `project/method — source URL — specific supported claim — scope limits — checked date`. AI-assisted curation does not establish that the maintainer read every item or independently reproduced its results.

## 5. Stable discovery and reuse

- [llms.txt](llms.txt) · [JSON manifest](agent-index.json) · [Sitemap](sitemap.xml) · [GitHub](https://github.com/ppchanning/agent-environments-and-evaluation)
Original commentary and compilation use [CC BY 4.0](LICENSE); third-party papers, software and data retain their own rights. Pages need no JavaScript or login. Discovery files do not guarantee indexing or citation by any search engine or agent.
