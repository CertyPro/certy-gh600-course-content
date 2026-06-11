# Glossary

Key terms for the GH-600 GitHub Agentic AI Developer exam. British English throughout.

### Agent
A system that pursues a goal by running a loop around a model: reasoning about the next step, acting (usually via a tool), observing the result and deciding whether to continue, validate, stop or hand back to a human.

### Planner
The component that decomposes a goal into an ordered set of steps, each with explicit, checkable success criteria.

### Executor
The component that carries out a single planned step, typically by calling a tool with the right arguments.

### Validator
The component that checks a step's result against its success criteria before the agent proceeds. The validator is what makes an agent's output trustworthy.

### ReAct loop
A reasoning pattern that interleaves reasoning and acting one step at a time (reason, act, observe, repeat), letting the agent adapt to each result. Contrast with plan-and-execute, which plans the whole sequence up front.

### Tool
A callable action exposed to the agent, with a typed input schema. Invoking a tool may have side effects (write a file, open a pull request). In MCP, the model invokes tools.

### MCP (Model Context Protocol)
An open protocol that standardises how a host application (an agent, IDE or assistant) connects to external context and tools through MCP servers. The host runs an MCP client per server; the server advertises its capabilities during initialisation.

### MCP resource vs MCP tool
A **resource** is read-only context (a file, record or query result) that the application or user attaches to the model's context. A **tool** is a callable action that may have side effects. Resources are read; tools act.

### stdio vs SSE transport
Two MCP transports. **stdio** has the host launch the server as a local subprocess and communicate over standard input and output - best for local tools. **SSE / streamable HTTP** connects to a remote server over HTTP with streamed messages - best for shared or hosted servers.

### Execution context
The conditions a tool runs under: its arguments, scope, credentials and environment. Designing the execution context with least privilege limits what a tool can do.

### Short-term memory
Also called working memory. The current context window and scratch state for the active run. Volatile - it does not persist beyond the run.

### Episodic memory
A durable record of past runs, events and decisions the agent can look back on across runs.

### Semantic memory
Durable facts and knowledge, typically stored as embeddings in a vector store and retrieved by similarity search.

### State serialisation
Writing the agent's run state (current step, plan, partial results) to a durable format so it can be rehydrated to resume the run later.

### Checkpoint
A saved snapshot of state at a safe point in the loop, so a long-running agent can recover after a crash or interruption without starting over.

### State lock
A mechanism that ensures only one agent writes to shared state at a time, preventing concurrent writes from corrupting it or causing lost updates.

### Eval dataset
A version-controlled set of representative tasks with expected outcomes, used to score the agent's behaviour and track changes over time.

### Rubric
A defined scoring scheme for an evaluation - for example exact-match and rule-based checks, or a fixed set of criteria for model-graded (LLM-as-judge) scoring.

### Trace
The ordered record of a single run: each reasoning step, tool call, input, output and timing. The primary tool for debugging an agent.

### Multi-agent orchestration
Coordinating several agents to accomplish a task, for example an orchestrator (supervisor) dispatching to specialised worker agents, or agents passing control through peer handoffs.

### Handoff
The point at which one agent passes work to another. A good handoff has an explicit contract: what data is passed, in what shape, and what the receiver is responsible for.

### Conflict resolution
The policy applied when two agents produce competing results - for example last-writer-wins, a defined merge rule, or escalation to the orchestrator or a human.

### Guardrail
Any control that constrains an agent's behaviour to keep it safe - input filters, output redaction, approval gates and audit logging are all guardrails.

### Input filter
A guardrail that validates and sanitises input before the agent acts, including defending against prompt injection by treating untrusted content as data rather than instructions.

### Output redaction
Removing secrets, tokens and personal data from output before it is logged or returned. No PII, passwords or tokens should ever reach logs.

### Approval gate
A guardrail that pauses the agent and requires a human to authorise a high-risk action (such as merging, deploying, deleting or spending) before it proceeds.

### Audit log
A record of what the agent did, with what inputs, on whose authority and with what outcome - enough to reconstruct a run, with secrets redacted.
