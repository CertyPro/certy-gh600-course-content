# Chapter 03 - Memory, State & GitHub Context

**Exam domain:** 3.0 (25% - the joint-largest domain)
**Certy lessons:** `gh-agentic-memory-architecture`, `gh-agentic-state-serialization`, `gh-agentic-github-context`
**Practice repos:** [certy-gh600-memory-state-lab](https://github.com/CertyPro/certy-gh600-memory-state-lab), [certy-gh600-github-control-plane-lab](https://github.com/CertyPro/certy-gh600-github-control-plane-lab)

---

## Teaching goal

By the end of this chapter the learner can name the three memory tiers and choose a store for each, serialise and rehydrate agent state, create checkpoints, and use GitHub issues, PRs and the API as both a context source and a control plane. This domain ties for the largest weight - budget time accordingly.

## Before you start

- Clone both labs: memory-state-lab and github-control-plane-lab.
- Keep the [memory-systems](../../cheat-sheets/memory-systems.md) and [github-as-control-plane](../../cheat-sheets/github-as-control-plane.md) cheat sheets open.
- Provision a scoped GitHub token (read-only to start) for the control-plane exercises.

## Running order

1. **Memory tiers (lesson `gh-agentic-memory-architecture`).** Define the three tiers and give each a home:
   - **Short-term / working memory** - the current context window and scratch state for this run. Volatile.
   - **Episodic memory** - a log of past runs, events and decisions the agent can look back on.
   - **Semantic memory** - durable facts and knowledge, often stored as embeddings in a vector store and retrieved by similarity.
   Discuss retrieval: recent items for short-term, event lookup for episodic, embedding search for semantic.
2. **State serialisation (lesson `gh-agentic-state-serialization`).** Separate **memory** (what the agent knows) from **state** (where the agent is in its run: current step, plan, partial results). Serialise state to a durable format, then rehydrate it to resume. Show a run stopped halfway and resumed from disk.
3. **Checkpoints.** Add checkpoints at safe points in the loop so a long run can recover after a crash or interruption without starting over. Discuss how often to checkpoint - too rarely loses work, too often costs overhead.
4. **GitHub as context (lesson `gh-agentic-github-context`).** Read issues, PRs, comments, commits, diffs and Actions runs through the API. Treat the issue body, labels and PR description as structured context for the planner. In the control-plane lab, drive the agent from an issue.
5. **Consistency and staleness.** GitHub state can change mid-run - a comment is added, a label changes, a PR is merged. Discuss re-reading at decision points and handling stale context.

## Key points to land

- **Memory** is what the agent knows; **state** is where it is in the run. Serialise state to resume; manage memory by tier.
- Three tiers: short-term (working), episodic (past events), semantic (durable knowledge, often vector-stored).
- Semantic memory typically uses embeddings and similarity search for retrieval.
- Checkpoints make long runs recoverable. Place them at safe points.
- GitHub is both a **context source** (read issues, PRs, diffs) and a **control plane** (the agent acts through issues, PRs and Actions).
- Re-read GitHub state at decision points to avoid acting on stale context.

## Common mistakes

- Conflating memory with state, so resumption logic gets tangled.
- Putting everything in the context window (short-term) and never persisting episodic or semantic memory.
- No checkpoints, so any crash means a full restart.
- Reading GitHub once at the start and never refreshing, then acting on stale data.
- Requesting broader GitHub token scopes than the task needs.

## Exam mapping

Domain 3.0 is 25% of the exam. Expect questions distinguishing the memory tiers, choosing stores and retrieval strategies, serialising/checkpointing state, and using GitHub artefacts as structured context and as a control plane. The memory-vs-state distinction is a frequent trap.

## Wrap-up

Learners now have an agent that reads from a GitHub issue, holds tiered memory and can resume from a checkpoint. Chapter 04 evaluates and debugs it.
