# Chapter 05 - Multi-Agent Systems & Orchestration

**Exam domain:** 5.0 (10%)
**Certy lessons:** `gh-agentic-multi-agent-orchestrator`, `gh-agentic-state-locking`
**Practice repo:** [certy-gh600-multi-agent-orchestration-lab](https://github.com/CertyPro/certy-gh600-multi-agent-orchestration-lab)

---

## Teaching goal

By the end of this chapter the learner can describe orchestration topologies, define clean handoffs between agents, protect shared state with locking, resolve conflicts between agents, and judge when multiple agents are worth the added complexity.

## Before you start

- Clone the multi-agent-orchestration-lab.
- Keep the [orchestration-patterns cheat sheet](../../cheat-sheets/orchestration-patterns.md) open.
- Reuse the single agent from earlier chapters as a worker.

## Running order

1. **When to go multi-agent.** Start with the trade-off: more agents mean more coordination, more state to share and more ways to fail. Use multiple agents when roles are genuinely distinct or work can run in parallel. Otherwise keep one agent.
2. **Topologies (lesson `gh-agentic-multi-agent-orchestrator`).** Compare:
   - **Orchestrator / supervisor and workers** - a coordinator decomposes the task, dispatches to specialised workers and assembles the result.
   - **Peer handoff** - agents pass control to one another in sequence, each owning a stage.
   Draw both (see [`diagrams/`](../../diagrams)).
3. **Handoffs and contracts.** Define a clear contract for each handoff: what data is passed, in what shape, and what the receiver is responsible for. Loose handoffs are where multi-agent systems break.
4. **Shared state and locking (lesson `gh-agentic-state-locking`).** When agents share state, concurrent writes can corrupt it. Apply a **state lock** so only one agent writes at a time. Show a race without a lock, then the same scenario with one.
5. **Conflict resolution.** When two agents produce competing results, decide the policy: last-writer-wins, a merge rule, or escalate to the orchestrator or a human. Make the policy explicit.

## Key points to land

- Add agents only when roles are distinct or work parallelises. Complexity is a real cost.
- Two main topologies: orchestrator-and-workers, and peer handoff.
- Every handoff needs an explicit contract (data, shape, responsibility).
- Shared state needs a **lock** to prevent concurrent writes from corrupting it.
- Conflicts need a stated resolution policy - do not leave it to chance.

## Common mistakes

- Reaching for multiple agents when one would be simpler and safer.
- Vague handoffs where the receiver does not know what it was given or owns.
- Unlocked shared state, leading to lost updates and corruption under concurrency.
- No conflict policy, so the last agent to write silently wins by accident.
- An orchestrator with no stop condition, so coordination loops forever.

## Exam mapping

Domain 5.0 is 10% of the exam. Expect questions on topology choice (orchestrator vs peer handoff), handoff design, state locking to prevent concurrent corruption, conflict resolution, and judging when multi-agent is justified.

## Wrap-up

Learners run an orchestrator dispatching to workers over locked shared state. Chapter 06 puts guardrails around the whole system.
