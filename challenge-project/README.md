# GH-600 Capstone - A Supervised, Governed Agent

> Build, supervise, and govern an autonomous agent in a GitHub-driven delivery workflow.

This is the capstone for the GH-600 GitHub Agentic AI Developer course. You will extend the [agent-starter](https://github.com/CertyPro/certy-gh600-agent-starter) into a single agent that touches **every exam domain**: it reads a GitHub issue, plans, validates, calls an MCP tool, persists memory and state, runs an evaluation, and enforces guardrails with a human approval gate.

Complete the six chapters in [`../labs`](../labs) first. This project ties them together.

---

## The brief

Starting from the agent-starter, build an agent that, given a GitHub issue, completes a small, well-scoped task (for example: read an issue describing a required change, propose it as a pull request) under full supervision and governance.

### The agent must

1. **Read a GitHub issue** as its goal and context (issue body, labels), using GitHub as a context source.
2. **Plan** the task into ordered steps with explicit success criteria.
3. **Validate** each step's result before proceeding, with a step budget and a stop condition.
4. **Call an MCP tool** to perform a real action, with a typed input schema and least-privilege execution context.
5. **Persist memory and state** - tiered memory plus serialised state with at least one checkpoint, so the run can resume.
6. **Run an evaluation** - a small eval dataset scored by a rubric, executed in CI.
7. **Enforce guardrails** - validate and sanitise input (defend against prompt injection), redact secrets and PII from output and logs, and pause at a **human approval gate** before any high-risk action.
8. **Write an audit log** of what it did, with what inputs, on whose authority and the outcome (redacted).

---

## Step-to-domain map

Each step maps to an exam domain so you can see the whole syllabus exercised at once.

| Step | What you build | Domain |
| --- | --- | --- |
| Plan with success criteria; validate each step; step budget and stop condition | Planner / executor / validator loop | 1.0 Agent Architecture, Planning & Validation (15%) |
| Call an MCP tool with a typed schema and least-privilege context | Tool integration over a chosen transport | 2.0 Tooling, MCP Servers & Execution Context (25%) |
| Read the issue as context; persist tiered memory; serialise state; checkpoint | Memory, state and GitHub context | 3.0 Memory, State & GitHub Context (25%) |
| Eval dataset + rubric in CI; capture a trace; debug from it | Evaluation, debugging and iteration | 4.0 Evaluation, Debugging & Iteration (15%) |
| (Optional extension) split into orchestrator + worker with a state lock | Multi-agent orchestration | 5.0 Multi-Agent Systems & Orchestration (10%) |
| Input filter; output redaction; approval gate; audit log; least privilege | Governance and guardrails | 6.0 Governance, Guardrails & Compliance (10%) |

> The single-agent build covers domains 1, 2, 3, 4 and 6. To exercise domain 5 as well, take the optional extension and split the worker out under an orchestrator with a state lock (see [Chapter 05](../labs/chapter-05-multi-agent-orchestration)).

---

## Deliverables

Submit all four:

1. **The repository** - your extended agent-starter, with a clear README explaining how to run it.
2. **A green CI run** - the evaluation suite (and tests) passing in GitHub Actions, with a link to the run.
3. **An eval report** - the dataset, the rubric, and the scores, showing the agent meets the success criteria. Note any failures you found and fixed.
4. **A trace** - the ordered record of one full run (reasoning steps, tool calls, inputs, outputs), showing the plan, the MCP tool call, the validation, the approval gate and the redacted audit entries.

---

## Acceptance checklist

- [ ] Agent reads a real GitHub issue as its goal and context.
- [ ] Plan has explicit, checkable success criteria.
- [ ] Validator gates each step; a step budget and stop condition are in place.
- [ ] At least one MCP tool is called with a typed input schema and least-privilege credentials.
- [ ] Memory is tiered; state is serialised; at least one checkpoint allows resumption.
- [ ] An eval dataset with a rubric runs in CI and passes (green run linked).
- [ ] Input is validated and sanitised; prompt-injection defence is in place.
- [ ] Secrets and PII are redacted from all output and logs.
- [ ] A human approval gate blocks the high-risk action until sign-off.
- [ ] An audit log records who, what, when, authority and outcome (redacted).
- [ ] Eval report and a full trace are included.

---

## Tips

- Keep the task small. The marking is on supervision and governance, not on the size of the change the agent makes.
- Treat the issue body as **untrusted** - it is the most likely prompt-injection vector.
- Redact before you log, not after. Never let a token reach the log in the first place.
- Make the approval gate genuinely block - the agent should wait, not assume approval.
- Read your own trace before submitting; it is the fastest way to spot a missing guardrail.

When your mock-exam scores are consistently above the pass mark and this capstone is complete, you are ready to book the official GH-600 exam. Good luck.
