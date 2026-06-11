# Chapter 06 - Governance, Guardrails & Compliance

**Exam domain:** 6.0 (10%)
**Certy lessons:** `gh-agentic-input-safeguards`, `gh-agentic-output-redaction`
**Practice repo:** [certy-gh600-governance-guardrails-lab](https://github.com/CertyPro/certy-gh600-governance-guardrails-lab)

---

## Teaching goal

By the end of this chapter the learner can add input safeguards (including prompt-injection defences), redact sensitive output, insert human approval gates for high-risk actions, keep an audit log, and enforce least privilege - the controls that make an agent safe to run in a real delivery workflow.

## Before you start

- Clone the governance-guardrails-lab.
- Keep the [governance-guardrails cheat sheet](../../cheat-sheets/governance-guardrails.md) open.
- Bring the agent from earlier chapters - you will wrap it in guardrails.

## Running order

1. **Input safeguards (lesson `gh-agentic-input-safeguards`).** Validate and sanitise every input. Then address **prompt injection**: an agent that reads untrusted content (an issue body, a web page, a file) can be steered by instructions hidden in that content. Show an injection attempt and a defence - treat fetched content as data, not instructions; constrain what tools the agent may call; and keep the system instructions authoritative.
2. **Output redaction (lesson `gh-agentic-output-redaction`).** Before output is logged or returned, redact secrets, tokens and personal data. Demonstrate a redaction filter catching an API key in a tool result before it reaches the log. No PII, passwords or tokens in logs - ever.
3. **Approval gates.** For high-risk actions (merging, deploying, deleting, spending), pause and require a human to approve before the agent proceeds. Wire a gate into the loop and show the agent waiting for sign-off.
4. **Audit logs.** Record what the agent did, with what inputs, on whose authority and with what outcome. The audit log must itself respect redaction - log the action, not the secret.
5. **Least privilege and compliance.** Scope tool permissions and credentials to the task. Map the controls to compliance needs (data handling, traceability) and confirm nothing sensitive leaks into logs.

## Key points to land

- **Input filter** - validate and sanitise; treat untrusted content as data to defend against prompt injection.
- **Output redaction** - strip secrets, tokens and PII before logging or returning anything.
- **Approval gate** - a human authorises high-risk actions before the agent acts.
- **Audit log** - who, what, when, on whose authority, and the outcome (with secrets redacted).
- **Least privilege** - the smallest scope of tools and credentials the task needs.

## Common mistakes

- Trusting untrusted content as if it were instructions, opening the door to prompt injection.
- Logging raw tool output, leaking tokens or PII into logs.
- Auto-approving high-risk actions with no human in the loop.
- An audit log that records too little to reconstruct what happened, or one that itself contains secrets.
- Broad, standing credentials instead of task-scoped, least-privilege access.

## Exam mapping

Domain 6.0 is 10% of the exam. Expect questions on input validation and prompt-injection defence, output redaction, approval gates for high-risk actions, audit logging, and least-privilege scoping. The principle that secrets and PII must never reach logs comes up often.

## Wrap-up

Learners now have an agent wrapped in input safeguards, output redaction, an approval gate and an audit log. They are ready for the [capstone](../../challenge-project), which combines every chapter.
