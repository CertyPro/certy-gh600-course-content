# Cheat Sheet - Orchestration Patterns

**Domain 5.0 (10%)** | Lessons `gh-agentic-multi-agent-orchestrator`, `gh-agentic-state-locking` | Repo [multi-agent-orchestration-lab](https://github.com/CertyPro/certy-gh600-multi-agent-orchestration-lab)

## When to use multiple agents

Use multiple agents when **roles are genuinely distinct** or work **parallelises**. Otherwise one agent is simpler and safer. Every extra agent adds coordination, shared state and failure modes.

## Topologies

| Topology | Shape | Use when |
| --- | --- | --- |
| **Orchestrator / supervisor + workers** | A coordinator decomposes, dispatches to specialised workers, assembles results | Distinct sub-tasks; central control |
| **Peer handoff** | Agents pass control in sequence, each owning a stage | A pipeline of stages |

```
Orchestrator                         Peer handoff
   |  \  \                           A -> B -> C
worker worker worker                 (each owns a stage)
   \   |   /
   assemble result
```

## Handoffs

- Every handoff needs an explicit **contract**: what data is passed, in what shape, and what the receiver is responsible for.
- Loose handoffs are where multi-agent systems break.

## Shared state and locking

- Concurrent writes to shared state can **corrupt** it (lost updates).
- Apply a **state lock** so only one agent writes at a time.
- Lock the smallest scope for the shortest time needed.

## Conflict resolution

When two agents produce competing results, pick a policy in advance:

- last-writer-wins,
- a defined merge rule, or
- escalate to the orchestrator or a human.

Make the policy **explicit** - do not leave it to chance.

## Common mistakes

- Multi-agent when one agent would do.
- Vague handoffs; unlocked shared state; no conflict policy.
- An orchestrator with no stop condition.

## One-line recap

Add agents only when roles differ or work parallelises; **orchestrator+workers** or **peer handoff**; explicit handoff contracts; **lock shared state**; state a conflict policy.
