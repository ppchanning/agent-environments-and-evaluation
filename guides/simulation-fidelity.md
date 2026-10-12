**English** | [简体中文](simulation-fidelity.zh-CN.md)

# How to validate state and behavioral fidelity in agent simulators

**Updated: 2026-10-12 · Type: source-backed practical guide · Examples are not results measured by this collection.**

## Quick answer

Validate a simulator against **state transitions and decision-relevant behavior**, then evaluate the agent separately. A plausible reply, a valid JSON object and an agent success score each answer a different question.

This guide proposes a testing workflow; it reports no new benchmark results. [AppWorld](https://github.com/StonyBrookNLP/appworld) illustrates database-state task evaluation, while [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) illustrates ordered milestone and snapshot checks. Those designs inform validation without proving fidelity outside their specified settings.

## Three questions to keep separate

| Question | Evidence needed | Common overclaim |
| --- | --- | --- |
| Is the interface well formed? | Schema, argument and response checks | A valid response means the simulated behavior is correct |
| Is the simulated behavior faithful? | Matched reference transitions, invariants and side effects | Realistic wording means agreement with a real system |
| Did the agent complete the task? | Task-specific final state and process constraints | A completion message means the task succeeded |

A transfer claim needs an additional matched test on the intended reference system. If only simulation was tested, describe only that setting.

## A reusable validation matrix

| Dimension | A test to perform | Record |
| --- | --- | --- |
| Reset and reproducibility | Repeat from the same initial state and seed | Initial-state equality, expected randomness and divergent fields |
| Persistent state | Create an object, then query or modify it | State before/after and action dependency |
| Errors and invalid actions | Submit a known invalid request | Error type and unintended state changes |
| Side effects | Check protected objects after a successful action | Unexpected updates or deletions |
| Counterfactual sequences | Change an earlier action or its order | Whether later transitions respond consistently |
| Reference agreement | Apply matched actions to simulator and reference | State, output and error disagreements under the same conditions |
| Task outcome | Verify target and protected state | Passed checks, failed checks and unsupported requirements |

This matrix is a recommended specification. A reference may be a real system or a trusted executable mechanism; report which one. Without a reference, invariant tests establish internal consistency, not full real-world fidelity.

## Example: detect a misleading completion

Suppose an agent says it canceled a booking. Check that the targeted booking changed status, that no second booking changed, and that a later query shows the same result. Then test an invalid identifier. A simulator that returns “canceled” for every input can sound successful while failing all meaningful state checks.

This is an illustrative failure pattern, not a measured result from the listed projects.

## Report disagreements clearly

Keep the number of checked cases, failed cases and reference disagreements separate. For a numerical rate, include the denominator, task set, environment version and reference version. Do not compare rates obtained from unrelated task sets as a shared leaderboard.

A minimal record might contain `initial_state`, `actions`, `observations`, `final_state`, `reference`, `checks` and `limitations`. Unknown reference fields remain unknown. Preserve failure traces where redistribution is permitted, and keep private user data out of public examples.

## Read and reuse the sources

Use [guide-resources.json](../data/guide-resources.json) for curated designs and [guide-sources.json](../data/guide-sources.json) for source locations. For additional literature, fetch [papers.json](../data/papers.json) and follow its `appearances` to dated notes. Existing `verification` fields describe historical source checks, not simulator certification.

A read-only standard-library example:

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

Continue to the [state-verification reading path](../topics/state-and-testing.md). Cite original projects for their mechanisms and this guide for the proposed comparison workflow. This collection uses AI-assisted curation and has not independently reproduced the projects.

## Primary sources

- `appworld` — [AppWorld](https://github.com/StonyBrookNLP/appworld) · official-project-documentation · Initial state; state checkpointing; Evaluating the Agent; development restrictions
- `toolsandbox` — [ToolSandbox](https://github.com/apple-aiml-research/ToolSandbox) · official-project-documentation · Scenario definition; milestones; evaluation
- `mirrorapi` — [StableToolBench-MirrorAPI: Modeling Tool Environments as Mirrors of 7,000+ Real-World APIs](https://aclanthology.org/2025.findings-acl.273/) · published-conference-paper · ACL Anthology abstract and linked paper

Sources checked on 2026-10-12 for the scoped descriptions above, without independent reproduction. Machine-readable records: [guide-sources.json](../data/guide-sources.json).
