<p align="center"><strong>English</strong> | <a href="README.zh-CN.md">简体中文</a></p>

<p align="center"><a href="https://ppchanning.github.io/agent-environments-and-evaluation/">Documentation site</a> · <a href="agent-index.md">Agent index</a> · <a href="llms.txt">llms.txt</a> · <a href="https://www.selfref.org/agents/curated.html">SelfRef Library</a></p>

<p align="center"><img src="assets/banner.svg" alt="Agent Simulation Environments" width="100%"></p>

<h1 align="center">Agent Simulation Environments</h1>
<p align="center"><strong>A research map for building, generating, and validating agent simulation environments</strong><br>Explore how interactive worlds are simulated, generated, and validated for AI agents.</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/content-CC_BY_4.0-6366f1" alt="Content license: CC BY 4.0"></a>
  <a href="topics/README.md"><img src="https://img.shields.io/badge/focus-simulation_%7C_generation_%7C_fidelity-0284c7" alt="Simulation, environment generation and fidelity"></a>
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/README-English_%2B_简体中文-334155" alt="README available in English and Simplified Chinese"></a>
</p>

<p align="center"><a href="#updates">Updates</a> · <a href="#start-here">Start here</a> · <a href="#explore-the-landscape">Topic map</a> · <a href="#selected-reading">Selected reading</a> · <a href="resources/papers.md">Full bibliography</a> · <a href="digests/README.md">Archives</a> · <a href="CONTRIBUTING.md">Contribute</a></p>

**Find interactive, scalable, and verifiable simulation environments for agents.**

This repository focuses on **Agent Simulation Environments**: organizing states, actions, observations, feedback, and transition mechanisms from software systems, tool services, and task worlds into simulated worlds that agents can interact with repeatedly. Its central questions are how these worlds are built, how they can be generated automatically, how they preserve behavioral consistency, and under what conditions training and testing results can transfer to real systems.

The collection brings together papers and technical reading on stateful software simulators, API and tool-service simulation, browser and terminal task environments, trace-driven simulation, language world models, and verifiable environment generation. Tool protocols help explain simulation interfaces; state verification, counterfactual trajectories, and execution evaluation help assess whether simulated worlds and their feedback are trustworthy.

Use the collection to choose environment designs, compare the conditions suited to programmatic and model-driven simulation, find state and behavioral validation methods, and build your own simulation research bibliography. Reading notes retain the problem, method, author-reported evidence, limitations, and original source, helping you judge which research claims a simulator can support.

## Updates

<!-- updates-daily:start -->
- **2026-10-16** — Added [5 papers in 1 issue](digests/agent-environments/2026/2026-10-16.md): shared-state environments, tool emulation and simulator fidelity. Newly cataloged work includes earlier publications.
- **2026-10-15** — Added [5 papers in 1 issue](digests/agent-environments/2026/2026-10-15.md): rulebook world models, executable tool environments and failure-aware simulation. Testing evidence retains its limits.

- **2026-10-14** — Added [5 papers in 1 issue](digests/agent-environments/2026/2026-10-14.md): terminal environment generation, recorded-world replay and failure diagnosis. Real API tests inform simulation validation.

- **2026-10-13** — Added [5 papers in 1 issue](digests/agent-environments/2026/2026-10-13.md): cloud emulator synthesis, fidelity and black-box behavior checks. Real-service tests provide validation references.

- **2026-10-12** — Added [5 papers in 1 issue](digests/agent-environments/2026/2026-10-12.md): simulation feedback, API dependencies and flaky tests. Also launched [3 bilingual guides](guides/simulation-environment-selection.md), [1 Agent index](agent-index.md), [1 Skill](skills/agent-simulation-selection/SKILL.md) and a Pages reading site; listed in 2 Skill directories and connected to the [SelfRef Library](https://www.selfref.org/agents/curated.html).

- **2026-10-11** — Added [5 papers in 1 new issue](digests/agent-environments/2026/2026-10-11.md) — Stateful API exploration, hidden side effects & structural coverage. Real-service testing informs simulation validation.

- **2026-10-10** — [5 simulation & validation resources](digests/agent-environments/2026/2026-10-10.md) — API testing & task validation.

<!-- updates-daily:end -->

Last 7 days here; [full update history](CHANGELOG.md). Earlier entries follow material dates, backfilled on **2026-10-10**, when this repository launched.

<!-- updates-milestones:start -->
- 📚 **2026-10-12** — [SelfRef Library](https://www.selfref.org/agents/curated.html) launched: search across 2 collections, with 6 bilingual guides and 2 Skill downloads.
- 🧭 **2026-10-12** — [Three core guides and Agent reading entry points](agent-index.md), with complete English / Chinese versions and a [public reading site](https://ppchanning.github.io/agent-environments-and-evaluation/).
- 🚀 **2026-10-10** — [Launched](https://github.com/ppchanning/agent-environments-and-evaluation/commit/af1062e) with [43 resources](resources/papers.md) and [4 simulation reading paths](topics/README.md); added [English / Chinese homepages](README.zh-CN.md) and [update history](CHANGELOG.md).
<!-- updates-milestones:end -->

## Core guides and agent access

Three core guides, each available in English and Chinese, with primary sources, scope limits and reusable templates.

| Guide | What you get |
| --- | --- |
| [How to choose an agent simulation environment](guides/simulation-environment-selection.md) | Compare stateful simulators, mirrored tools, generated environments and learned worlds by the behavior a task needs. |
| [How to generate verifiable agent simulation environments](guides/environment-generation.md) | A design workflow from task specification to executable state, reset, verifiers and held-out validation. |
| [How to validate state and behavioral fidelity in agent simulators](guides/simulation-fidelity.md) | A practical test matrix for transitions, side effects, counterfactual traces, task success and transfer claims. |

[Read on Pages](https://ppchanning.github.io/agent-environments-and-evaluation/) · [Agent index](agent-index.md) · [JSON manifest](agent-index.json) · [llms.txt](llms.txt)

## Installable agent skill

[Read the skill](skills/agent-simulation-selection/SKILL.md): a research workflow connecting guides, JSON evidence and primary sources. Example: Choose a stateful simulator and propose tests for hidden side effects and reset.

```sh
npx skills add ppchanning/agent-environments-and-evaluation --skill agent-simulation-selection
```

Install with the Skills CLI into a supported agent; the first run downloads the CLI. The skill itself is a read-only research workflow, returning evidence, unknowns and next checks. Directory indexing is verified separately from installability.

Find this skill on [Agent Skill Hub](https://agentskillhub.dev/u/ppchanning/sk/agent-simulation-selection) and [askill](https://askill.sh/skills/gh/ppchanning/agent-environments-and-evaluation/@agent-simulation-selection). For repository navigation and Q&A, use [DeepWiki](https://deepwiki.com/ppchanning/agent-environments-and-evaluation); its generated explanations should be checked against the cited source files.

## Start here

| Your question | Where to start | What you get |
| --- | --- | --- |
| How can agent simulation environments be built or generated automatically? | [Simulation design and environment generation](topics/environment-generation.md) | Research directions in stateful simulators, programmatic generation, trace-driven simulation, and language world models |
| Does a simulation preserve a real system's state and behavior? | [State and behavioral verification](topics/state-and-testing.md) | State transitions, hidden dynamics, behavioral consistency, and validation methods |
| How can an agent's tools and services be simulated? | [Tool interfaces and service simulation](topics/tool-protocols.md) | Reading paths through MCP / API interfaces, tool feedback, and stateful service behavior |
| How should simulation quality and agent execution be evaluated? | [Simulation validity and execution evaluation](topics/agent-evaluation.md) | Ways to compare simulation fidelity, trace checks, result verification, and transfer limitations |
| Which simulation studies are worth following now? | [Latest reading notes](digests/agent-environments/2026/2026-10-16.md) · [Archives](digests/README.md) | Recommendations, method explanations, evidence limitations, and original sources |
| How can I organize my own related-work table? | [Full bibliography](resources/papers.md) · [JSON data](data/README.md) | Deduplicated identifiers, sources, versions, and appearance records for filtering and further reading |

For researchers building agent training and testing environments, developers of software and tool-service simulators, world-model and synthetic-environment researchers, and systems developers who need to verify simulation state and behavior. **The homepage is available in English and [Simplified Chinese](README.zh-CN.md). Most existing research notes and supporting archives are in Chinese; the three core guides and Agent index are fully bilingual, retaining original English titles and source links.**

## Explore the landscape

### Simulation design & environment generation

Study how software, tool services, and task workflows become interactive simulated worlds. This area covers stateful simulators, automatically generated environments, trace-driven simulation, and language world models. Compare initialization, state transitions, task generation, and feedback mechanisms, along with the tradeoffs between scale and behavioral fidelity.

**Start reading:** [Simulation design & environment generation](topics/environment-generation.md)

### State & behavioral fidelity

Simulation quality depends on whether action sequences produce reasonable state changes, hidden dynamics remain consistent, error conditions are preserved, and behavior drifts during long interactions. This topic connects research on state checks, differential testing, counterfactual trajectories, and behavioral validation.

**Start reading:** [State & behavioral verification](topics/state-and-testing.md)

### Tool interfaces & service simulation

MCP / API protocols define how agents interact with environments; simulators also need to implement the state and service behavior behind those interfaces. This topic covers tool calls, service feedback, interface testing, and simulation of real APIs, supporting the study and validation of the interaction layer.

**Start reading:** [Tool interfaces & service simulation](topics/tool-protocols.md)

### Simulation validity & execution evaluation

Use execution traces, task outcomes, process metrics, and comparisons with real systems to assess whether simulation feedback is reliable and how broadly the measured agent capabilities apply. The focus is on fidelity, reproducibility, environment bias, and transfer conditions, with original evidence retained for those judgments.

**Start reading:** [Simulation validity & execution evaluation](topics/agent-evaluation.md)

## Selected reading

These examples highlight simulation design, generation, and validation. Title links point to original sources; the questions are this collection's reading prompts. Full metadata and associated reading issues are available in the [paper catalog](resources/papers.md).

| Reading question | Selected resource | Related topics |
| --- | --- | --- |
| How can interaction traces become executable simulated worlds? | [From Traces to Agentic Worlds](https://arxiv.org/abs/2610.06100) | Environment generation, world models |
| How can skill-training environments with verification mechanisms be generated automatically? | [SkillGym](https://arxiv.org/abs/2609.37539) | Environment generation, tool use |
| How can a stateful software simulator be checked for behavioral consistency? | [CTE-Bench](https://arxiv.org/abs/2609.36647) | Simulation, state, evaluation |
| What system evidence should be checked after an agent claims completion? | [The Agent Said It Was Done. The Database Disagreed.](https://huggingface.co/blog/microsoft/thinkingbox) | Task verification, real system state |
| How can the interaction behavior of real APIs be simulated? | [StableToolBench-MirrorAPI](https://aclanthology.org/2025.findings-acl.273/) | Tool-service simulation, API environments |

## What a reading note gives you

Each issue is organized around the following questions, with depth determined by the original evidence available:

- **Problem and setting:** Which system, tool, or task is simulated, why simulation is needed, and what real system serves as a reference.
- **Method and system:** How states, actions, observations, and feedback are represented; how the environment is generated and updated; and which mechanisms matter.
- **Author-reported evidence:** Which traces, tasks, real-system comparisons, or verification mechanisms are used, and which claims about simulation quality and agent capabilities the results support.
- **Limitations and transfer conditions:** Gaps between simulated and real execution, behaviors outside the study's coverage, and conditions needed to interpret the results.
- **Further reading:** Original paper links, version information, and suggested sections to read first.

Topic indexes support comparison across methods, dated archives support continued tracking, and structured bibliographies support local search. Together, they help you build your own map of related work and methods.

## Collection at a glance

<!-- collection-stats:start -->
As of **2026-10-16**: **17 reading issues · 73 deduplicated resources · 4 topical reading paths**.

The reading archive covers 2026-09-28 through 2026-10-16, with possible gaps within that date range. New and revised material is archived by date, with current entry points, topic indexes, and the deduplicated bibliography maintained together.
<!-- collection-stats:end -->

## How to use this repository

1. **Get started:** Choose a practical question, select papers from its topic page, and use the reading notes to identify what to focus on.
2. **Keep up:** Read the latest issue and revisit the archives to track how methods in the same area change over time.
3. **Design a simulation environment:** Compare states, actions, feedback, environment generation, and fidelity checks across studies. Return to original sources to confirm their applicable conditions.
4. **Organize related work:** Download [papers.json](data/papers.json), deduplicate using identifiers, versions, and appearance records, and build your literature table. Optional fields may be missing; see the [data guide](data/README.md).
5. **Contribute resources:** Suggest sourced papers or technical cases, improve topic classifications and metadata, or correct evidence. See the [contribution guide](CONTRIBUTING.md) and [issues](https://github.com/ppchanning/agent-environments-and-evaluation/issues).

## Repository map

```text
digests/       # Paper reading notes: channel / year / date
topics/        # Simulation design, generation, fidelity, services, and execution validation
resources/     # Full bibliography and original-source entry points
data/          # Deduplicated JSON bibliography and field definitions
docs/          # Editorial policy, sharing guidance, and design references
skills/        # Installable evidence-guided agent workflow
templates/     # Consistent templates for new material
.github/       # Resource suggestions, corrections, and pull request templates
```

## Sources, contributions & citation

This collection provides papers and technical resources for reading and comparing system designs. Executable environments, benchmark implementations, and evaluation results should be obtained from their original projects. Curation distinguishes preprints, published papers, and official cases, preserving sources, versions, and evidence limitations. Content is curated with AI assistance and does not imply that the maintainer has completed the reading or independently replicated results. See the [editorial policy](docs/editorial-policy.md).

Contributions of papers, technical cases, reading paths, and corrections are welcome; see [CONTRIBUTING](CONTRIBUTING.md). Original commentary and compilation are licensed under [CC BY 4.0](LICENSE); third-party works retain their respective rights. Cite original papers for scientific claims. To cite this collection, use [CITATION.cff](CITATION.cff).

**Related collection:** [AI4Science Observatory](https://github.com/ppchanning/ai4science-observatory) focuses on AI scientific discovery, scientific agents, scientific software, and remote physical experiments.

[Sharing guide](docs/sharing.md) · [Design references](docs/design-references.md)
