# Cheat Sheet - Memory Systems

**Domain 3.0 (25%)** | Lessons `gh-agentic-memory-architecture`, `gh-agentic-state-serialization` | Repo [memory-state-lab](https://github.com/CertyPro/certy-gh600-memory-state-lab)

## Memory vs state (exam trap)

- **Memory** = what the agent knows.
- **State** = where the agent is in its run (current step, plan, partial results).
- You **serialise state** to resume a run; you **manage memory** by tier.

## The three memory tiers

| Tier | What it holds | Lifetime | Typical store / retrieval |
| --- | --- | --- | --- |
| **Short-term / working** | Current context window, scratch state | This run only (volatile) | In-context; recency |
| **Episodic** | Past runs, events, decisions | Across runs | Event log; lookup by run/event |
| **Semantic** | Durable facts and knowledge | Long-lived | Vector store; **embedding similarity search** |

## State serialisation and checkpoints

- **Serialise** state to a durable format, then **rehydrate** to resume.
- **Checkpoint** at safe points in the loop so a long run recovers after a crash without restarting.
- Checkpoint frequency is a trade-off: too rare loses work, too often adds overhead.

## Retrieval strategies

- Short-term: keep recent, relevant items in context.
- Episodic: retrieve specific past events when relevant.
- Semantic: embed the query and retrieve by similarity from the vector store.

## Common mistakes

- Conflating memory and state.
- Keeping everything in the context window and never persisting episodic/semantic memory.
- No checkpoints, so any crash means a full restart.

## One-line recap

Three tiers - **short-term, episodic, semantic** (semantic = embeddings + similarity). **Memory is knowledge; state is position.** Serialise + checkpoint to resume.
