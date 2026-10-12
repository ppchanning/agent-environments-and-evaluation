**English** \| [简体中文](simulation-environment-selection.zh-CN.md)

# How to choose an agent simulation environment

**Updated: 2026-10-12 · Type: source-backed practical guide · Examples are not results measured by this collection.**

## Quick answer

Choose an agent simulation environment by **which state and behaviors must remain correct across an action sequence**. If database changes determine success, prioritize explicit state and executable checks. If broad interaction diversity matters, generated or model-driven worlds may help, but their transitions still need an independent reference.

This guide is a design and reading map. The repository does not ship these simulators or certify their real-world fidelity. The primary documentation below was checked on 2026-10-12; no independent execution was performed.

## Compare four entry points

| Entry | Environment approach | Why read it | Boundary to preserve |
| --- | --- | --- | --- |
| [AppWorld](https://github.com/StonyBrookNLP/appworld) | A controllable world of apps backed by state | Study tasks, database state, checkpointing and task evaluation | App simulation is not operation on actual user accounts; checkpoint privileges affect fair comparisons |
| [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) | Stateful tool interaction with scenario and milestone evaluation | Study persistent state and ordered interaction requirements | Its scenarios and checks do not establish fidelity for arbitrary external services |
| [EnvScaler](https://github.com/RUC-NLPIR/EnvScaler) | Programmatic synthesis of executable, stateful tool environments | Study how environment generation connects to interaction | Generated executability alone does not establish agreement with a real service |
| [StableToolBench-MirrorAPI](https://aclanthology.org/2025.findings-acl.273/) | Mirrored tool environments motivated by real API behavior | Study the design of tool-service simulation | Read the paper's construction and evaluation conditions before transferring conclusions |

This table describes approaches, not comparable performance scores. A tool protocol describes an interface; the simulator must also define the state transitions behind that interface.

## Match an environment to a task

| Task requirement | Prefer to inspect | Deciding check |
| --- | --- | --- |
| Create, update or delete objects | Explicit stateful simulator | Does the final state and every protected object satisfy the task? |
| Long sequences with dependencies | Persistent state plus trace checks | Do earlier actions change later preconditions and observations? |
| Many new tool scenarios | Programmatic environment generation | Are generated tasks solvable, diverse and independently verifiable? |
| Flexible textual worlds | Learned or language-model transitions | Do reference traces and counterfactual actions expose inconsistent dynamics? |
| Transfer to a real system | A reference system and matched test cases | What succeeds in simulation but fails under real interfaces or constraints? |

The last two rows are selection heuristics, not claims that a named project has passed those checks.

## A minimal environment contract

Before choosing a project, write down:

- **State:** persisted objects, hidden variables and ownership between episodes.
- **Actions:** tool schemas, units, preconditions and side effects.
- **Observations:** what the agent sees, including errors and delays.
- **Reset:** which state is restored and what randomness remains.
- **Verifier:** how task completion and unintended changes are checked.
- **Reference:** a real system, formal mechanism or trusted executable specification, if available.

For a calendar task, success could require one new event with specified fields while existing events remain unchanged. That is a generic illustrative task, not a reported benchmark result.

## Return a useful recommendation

A recommendation should include the intended task, environment type, state requirements, candidate source, validation gap and access or license conditions. If no reference system is available, state that fidelity remains unestablished rather than assign a numerical trust score.

Continue to [Environment generation](environment-generation.md) and [Simulation fidelity](simulation-fidelity.md). For machine-readable discovery, use [agent-index.json](../agent-index.json) and [guide-resources.json](../data/guide-resources.json); the broader [papers.json](../data/papers.json) preserves historical reading records.

## Primary sources

- `appworld` — [AppWorld](https://github.com/StonyBrookNLP/appworld) · official-project-documentation · Initial state; state checkpointing; Evaluating the Agent; development restrictions
- `toolsandbox` — [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) · official-project-documentation · Scenario definition; milestones; evaluation
- `envscaler` — [EnvScaler](https://github.com/RUC-NLPIR/EnvScaler) · official-project-documentation · Overview; environment synthesis and agent interaction modules
- `mirrorapi` — [StableToolBench-MirrorAPI: Modeling Tool Environments as Mirrors of 7,000+ Real-World APIs](https://aclanthology.org/2025.findings-acl.273/) · published-conference-paper · ACL Anthology abstract and linked paper

Sources checked on 2026-10-12 for the scoped descriptions above, without independent reproduction. Machine-readable records: [guide-sources.json](../data/guide-sources.json).
