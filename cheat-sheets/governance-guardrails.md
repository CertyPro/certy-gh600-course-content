# Cheat Sheet - Governance & Guardrails

**Domain 6.0 (10%)** | Lessons `gh-agentic-input-safeguards`, `gh-agentic-output-redaction` | Repo [governance-guardrails-lab](https://github.com/CertyPro/certy-gh600-governance-guardrails-lab)

## The four controls

| Control | What it does | Where it sits |
| --- | --- | --- |
| **Input filter** | Validate and sanitise input; defend against prompt injection | Before the agent reasons |
| **Output redaction** | Strip secrets, tokens and PII | Before output is logged or returned |
| **Approval gate** | Human authorises high-risk actions first | Before a high-risk tool call |
| **Audit log** | Record who, what, when, on whose authority, outcome | Around every significant action |

## Input safeguards and prompt injection

- Validate and sanitise every input.
- **Prompt injection:** untrusted content (issue body, web page, file) may hide instructions that steer the agent.
- Defences: treat fetched content as **data, not instructions**; keep system instructions authoritative; constrain which tools the agent may call when handling untrusted input.

## Output redaction

- Redact secrets, tokens and personal data before anything is logged or returned.
- **No PII, passwords or tokens in logs - ever.**
- The audit log must respect redaction too: log the action, not the secret.

## Approval gates

- For high-risk actions (merge, deploy, delete, spend), pause and require **human sign-off** before proceeding.
- The agent waits; it does not assume approval.

## Audit logs

Record: who acted, what they did, with what inputs, on whose authority, and the outcome - enough to reconstruct the run, with secrets redacted.

## Least privilege and compliance

- Scope tools and credentials to the task.
- Map controls to compliance needs (data handling, traceability).

## One-line recap

**Filter in, redact out, gate the risky, log everything (redacted), least privilege throughout.** Treat untrusted content as data, never as instructions.
