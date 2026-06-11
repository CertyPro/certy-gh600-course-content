# Practice Questions

These eight sample multiple-choice questions span the six GH-600 domains. They are a warm-up, not the real thing.

> **Sit the full mock exam at [certy.pro](https://certy.pro).** The mock exam is timed, weighted to match the real domains, and gives a readiness score. Use these samples to check your understanding of each domain, then move to the mock exam.

Try each question before opening the answer.

---

### Q1 (Domain 1.0 - Agent Architecture)

In a planner / executor / validator architecture, which component is responsible for confirming a step's result meets its success criteria before the agent continues?

- A. Planner
- B. Executor
- C. Validator
- D. Orchestrator

<details><summary>Answer</summary>

**C - Validator.** The validator checks the result against the success criteria set by the planner before the loop proceeds. The planner decomposes the goal; the executor carries out the step. Without a validator there is no basis for trusting the result.
</details>

---

### Q2 (Domain 1.0 - Agent Architecture)

An agent keeps calling tools and never finishes. Which guard most directly prevents this?

- A. A larger context window
- B. A step budget with a stop condition
- C. A faster model
- D. More detailed tool descriptions

<details><summary>Answer</summary>

**B - A step budget with a stop condition.** Unbounded loops are prevented by capping steps and defining when the loop must stop. The other options may help quality or speed but do not bound the loop.
</details>

---

### Q3 (Domain 2.0 - Tooling & MCP)

In the Model Context Protocol, what is the key difference between a **tool** and a **resource**?

- A. Tools are remote; resources are local
- B. A tool is a callable action that may have side effects; a resource is read-only context attached to the model
- C. Tools are free; resources are billed
- D. There is no difference; the terms are interchangeable

<details><summary>Answer</summary>

**B.** A tool is an action the model can invoke and it may change things. A resource is read-only context (a file, record or query result) the application or user attaches to the model's context. This distinction is one of the most commonly tested points in domain 2.0.
</details>

---

### Q4 (Domain 2.0 - Tooling & MCP)

You are connecting an agent to an MCP server that runs as a shared, remote service. Which transport is most appropriate?

- A. stdio
- B. HTTP with Server-Sent Events (SSE) / streamable HTTP
- C. A local Unix pipe only
- D. Direct database connection

<details><summary>Answer</summary>

**B - HTTP with SSE / streamable HTTP.** Remote, shared servers are reached over HTTP with streamed messages. **stdio** is for local servers the host launches as a subprocess.
</details>

---

### Q5 (Domain 3.0 - Memory, State & GitHub Context)

Which memory tier is best suited to durable facts retrieved by embedding similarity search?

- A. Short-term / working memory
- B. Episodic memory
- C. Semantic memory
- D. Checkpoint memory

<details><summary>Answer</summary>

**C - Semantic memory.** Semantic memory holds durable knowledge and is typically stored as embeddings in a vector store, retrieved by similarity. Short-term is the working context; episodic logs past events; "checkpoint memory" is not a tier (a checkpoint is a saved state snapshot).
</details>

---

### Q6 (Domain 3.0 - Memory, State & GitHub Context)

An agent reads a GitHub issue once at the start of a long run and acts on it 20 minutes later, but a maintainer has since added a clarifying comment. What is the core problem and best mitigation?

- A. Insufficient memory; add more RAM
- B. Stale context; re-read GitHub state at decision points
- C. A failed tool call; retry the tool
- D. A prompt-injection attack; redact the output

<details><summary>Answer</summary>

**B - Stale context.** GitHub state can change mid-run. Re-reading the relevant state at decision points (and re-planning if it changed) avoids acting on out-of-date context.
</details>

---

### Q7 (Domain 4.0 - Evaluation & Debugging)

A run produced confident but incorrect output. The trace shows the plan was sound and the tool returned correct data, but the final answer ignored it. Which failure type is this, and where do you fix it?

- A. Planning failure; fix the planner prompt
- B. Execution failure; fix the tool
- C. Validation gap; add or tighten the validator
- D. Transport failure; switch from stdio to SSE

<details><summary>Answer</summary>

**C - Validation gap.** The plan and tool were fine, but a wrong result was allowed through. Adding or tightening the validator so it checks the output against the tool data and success criteria is the fix.
</details>

---

### Q8 (Domain 5.0 and 6.0 - Orchestration & Governance)

Two worker agents write to the same shared state at the same time and one update is lost. Separately, an agent about to merge a PR proceeds with no human review. Which two controls address these problems respectively?

- A. A larger model; a faster CI runner
- B. A state lock; a human approval gate
- C. Output redaction; an eval dataset
- D. A new transport; a bigger step budget

<details><summary>Answer</summary>

**B - A state lock and a human approval gate.** A state lock serialises writes to shared state so updates are not lost (domain 5.0). An approval gate requires a human to authorise the high-risk merge before the agent proceeds (domain 6.0).
</details>

---

Ready for the real test? Take the timed, weighted mock exam at **[certy.pro](https://certy.pro)**.
