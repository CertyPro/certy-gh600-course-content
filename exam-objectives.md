# GH-600 Exam Objectives

The GH-600 GitHub Agentic AI Developer exam measures your ability to build, supervise and govern autonomous agents that operate inside a GitHub-driven delivery workflow. It is organised into six domains. The weights below are fixed and add up to 100%.

| Domain | Weight |
| --- | --- |
| 1.0 Agent Architecture, Planning & Validation | 15% |
| 2.0 Tooling, MCP Servers & Execution Context | 25% |
| 3.0 Memory, State & GitHub Context | 25% |
| 4.0 Evaluation, Debugging & Iteration | 15% |
| 5.0 Multi-Agent Systems & Orchestration | 10% |
| 6.0 Governance, Guardrails & Compliance | 10% |

Each domain below lists the skills you should be able to demonstrate, the matching Certy lessons, and the practice repository to use.

---

## 1.0 Agent Architecture, Planning & Validation (15%)

**You should be able to:**

- Describe the core agent loop and the responsibilities of the planner, executor and validator roles.
- Explain reasoning patterns such as ReAct (reason then act), plan-and-execute, and reflection.
- Decompose a goal into an ordered, verifiable plan with explicit success criteria.
- Decide when an agent should transition between reasoning, acting and validating, and when it should stop or hand control back to a human.
- Add validation steps that check tool output and intermediate state before the agent proceeds.
- Recognise failure modes such as looping, premature completion and unbounded steps, and design guards against them.

**Certy lessons:** `gh-agentic-reasoning-patterns`, `gh-agentic-transition-control`

**Practice repo:** [certy-gh600-agent-starter](https://github.com/CertyPro/certy-gh600-agent-starter)

---

## 2.0 Tooling, MCP Servers & Execution Context (25%)

**You should be able to:**

- Explain the Model Context Protocol (MCP) and the client-server relationship between a host (such as an agent or IDE) and an MCP server.
- Distinguish MCP **tools** (callable actions with side effects) from MCP **resources** (read-only context the host can attach).
- Describe MCP prompts and how a server advertises its capabilities during initialisation.
- Build a basic MCP server, register tools with typed input schemas, and return structured results.
- Choose and configure a transport - stdio for local processes, and HTTP with Server-Sent Events (SSE) or streamable HTTP for remote servers.
- Design the execution context an agent passes to a tool: arguments, scope, permissions and environment.
- Reason about least privilege when granting an agent access to tools.

**Certy lessons:** `gh-agentic-mcp-intro`, `gh-agentic-mcp-dev`, `gh-agentic-mcp-transports`

**Practice repo:** [certy-gh600-mcp-server-lab](https://github.com/CertyPro/certy-gh600-mcp-server-lab)

---

## 3.0 Memory, State & GitHub Context (25%)

**You should be able to:**

- Distinguish the memory tiers: short-term (working/context window), episodic (past runs and events) and semantic (durable facts and knowledge).
- Choose an appropriate store for each tier and explain retrieval strategies, including embedding-based recall for semantic memory.
- Serialise agent state to a durable format and rehydrate it to resume a run.
- Create checkpoints so a long-running agent can recover after failure or interruption.
- Use GitHub as a context source and control plane: read issues, pull requests, comments, commits, diffs and Actions runs through the API.
- Treat repository artefacts (issue bodies, labels, PR descriptions, files) as structured context for planning.
- Reason about consistency and staleness when GitHub state changes mid-run.

**Certy lessons:** `gh-agentic-memory-architecture`, `gh-agentic-state-serialization`, `gh-agentic-github-context`

**Practice repos:** [certy-gh600-memory-state-lab](https://github.com/CertyPro/certy-gh600-memory-state-lab), [certy-gh600-github-control-plane-lab](https://github.com/CertyPro/certy-gh600-github-control-plane-lab)

---

## 4.0 Evaluation, Debugging & Iteration (15%)

**You should be able to:**

- Build an evaluation dataset of representative tasks with expected outcomes.
- Define rubrics and scoring methods, including exact-match, rule-based checks and model-graded (LLM-as-judge) scoring.
- Capture and read traces - the ordered record of an agent's reasoning steps, tool calls and results.
- Use traces to locate where a run went wrong: a bad plan, a failing tool call, a hallucinated result or a validation gap.
- Run an evaluation suite in CI and track score regressions across changes.
- Iterate on prompts, tools and validation logic based on evidence from evals and traces.

**Certy lessons:** `gh-agentic-eval-frameworks`, `gh-agentic-trace-debugging`

**Practice repo:** [certy-gh600-evaluation-debugging-lab](https://github.com/CertyPro/certy-gh600-evaluation-debugging-lab)

---

## 5.0 Multi-Agent Systems & Orchestration (10%)

**You should be able to:**

- Describe orchestration topologies: a supervisor or orchestrator coordinating worker agents, and peer handoff patterns.
- Define clear roles and contracts so agents pass work cleanly through handoffs.
- Manage shared state between agents and apply state locking to prevent concurrent writes corrupting it.
- Detect and resolve conflicts when two agents produce competing results.
- Decide when multiple agents add value versus when a single agent is simpler and safer.

**Certy lessons:** `gh-agentic-multi-agent-orchestrator`, `gh-agentic-state-locking`

**Practice repo:** [certy-gh600-multi-agent-orchestration-lab](https://github.com/CertyPro/certy-gh600-multi-agent-orchestration-lab)

---

## 6.0 Governance, Guardrails & Compliance (10%)

**You should be able to:**

- Apply input safeguards: validate and sanitise inputs and defend against prompt injection from untrusted content.
- Redact sensitive output - secrets, tokens and personal data - before it is logged or returned.
- Insert approval gates so a human authorises high-risk actions before the agent proceeds.
- Maintain an audit log that records what the agent did, with what inputs, and on whose authority.
- Enforce least privilege and scope tool permissions to the task.
- Map controls to compliance needs and avoid storing PII, passwords or tokens in logs.

**Certy lessons:** `gh-agentic-input-safeguards`, `gh-agentic-output-redaction`

**Practice repo:** [certy-gh600-governance-guardrails-lab](https://github.com/CertyPro/certy-gh600-governance-guardrails-lab)

---

Sit the full mock exam at [certy.pro](https://certy.pro) to check your readiness against these objectives.
