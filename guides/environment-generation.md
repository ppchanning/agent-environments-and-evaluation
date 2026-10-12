**English** \| [简体中文](environment-generation.zh-CN.md)

# How to generate verifiable agent simulation environments

**Updated: 2026-10-12 · Type: source-backed practical guide · Examples are not results measured by this collection.**

## Quick answer

Generate an environment together with **an explicit state contract, a reset mechanism and an independently checkable task verifier**. Producing plausible tool responses alone does not establish a usable training world.

The workflow below is this collection's design recommendation. [EnvScaler](https://github.com/RUC-NLPIR/EnvScaler) provides a primary example of programmatic synthesis; [AppWorld](https://github.com/StonyBrookNLP/appworld) and [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) provide useful state and evaluation reference designs. This collection has not measured the quality of generated environments.

## Choose the generation mechanism

| Mechanism | What is generated | Useful when | Main validation need |
| --- | --- | --- | --- |
| Programmatic synthesis | Executable state logic, tools and tasks | State and constraints can be expressed in code | Check independent invariants and reference cases |
| Trace-guided construction | Dynamics inferred or designed from interaction records | Relevant reference interactions exist | Test unseen sequences; distinguish copied responses from reconstructed behavior |
| Model-driven transitions | Observations and state updates proposed by a model | Broader or less rigid interaction is needed | Audit contradictions, persistence and decision-relevant discrepancies |
| Hybrid environment | Executable core with generated peripheral responses | Some effects need exact control while others need diversity | Identify which component is authoritative for each state field |

These are methodological categories. They do not imply that all four mechanisms are implemented in this repository or in a single listed project.

## A six-stage workflow

1. **Specify the world.** Define domain objects, allowed actions, agent-visible observations, hidden state and the task's completion condition.
2. **Generate the implementation.** Keep authoritative state separate from narrative output. Document every state-changing action and error case.
3. **Generate task instances.** Supply an initial state, instruction and expected constraints. Include both valid tasks and deliberately invalid requests.
4. **Write independent checks.** Use reference implementations, fixed examples or separately reviewed invariants. A generator's own assertion that its task is correct is insufficient.
5. **Check reset and isolation.** Repeat an episode from the same seed, and run separate tasks without shared unintended state.
6. **Hold out cases.** Evaluate unfamiliar compositions, boundary values and altered action orders; keep training examples separate from assessment.

## Example: a synthetic inventory task

An illustrative task asks an agent to reserve two units of an item. The state contains stock, reservations and a request identifier. The environment contract says the reservation reduces available stock once and must not modify another item.

| Test | Expected property |
| --- | --- |
| Reserve within available stock | Exactly one corresponding reservation and stock change |
| Request more than available stock | Documented error; no unintended state change |
| Repeat the same request | Behavior follows the specified idempotency contract |
| Reset the episode | Original stock and empty episode-specific reservations |
| Reserve a different item afterwards | Correct dependency on the resulting state |

This is an example specification, not an implemented environment or an empirical result. Real APIs can have different idempotency and error semantics; copy neither without a reference.

## Keep verifiers independent of the generator

Separate task success from environment validity. An agent can pass a task in a simulator whose dynamics are incorrect. Keep a small collection of independently checked transition examples, inspect protected state, and record disagreements rather than averaging them into a single optimistic score.

Report the generation method, environment version, task distribution, rejected tasks and test coverage. Counts of generated environments do not establish diversity or fidelity. Use [Simulation fidelity](simulation-fidelity.md) for a concrete validation matrix.

## Reuse and reading path

Start with [EnvScaler's official implementation](https://github.com/RUC-NLPIR/EnvScaler). Compare its design with the source-linked examples in [guide-resources.json](../data/guide-resources.json), then explore the existing [environment-generation reading path](../topics/environment-generation.md). Historical notes retain their own verification limits; confirm claims against primary sources.

## Primary sources

- `envscaler` — [EnvScaler](https://github.com/RUC-NLPIR/EnvScaler) · official-project-documentation · Overview; environment synthesis and agent interaction modules
- `appworld` — [AppWorld](https://github.com/StonyBrookNLP/appworld) · official-project-documentation · Initial state; state checkpointing; Evaluating the Agent; development restrictions
- `toolsandbox` — [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) · official-project-documentation · Scenario definition; milestones; evaluation

Sources checked on 2026-10-12 for the scoped descriptions above, without independent reproduction. Machine-readable records: [guide-sources.json](../data/guide-sources.json).
