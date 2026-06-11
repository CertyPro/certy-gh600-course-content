# Cheat Sheet - GitHub as a Control Plane

**Domain 3.0 (25%)** | Lesson `gh-agentic-github-context` | Repo [github-control-plane-lab](https://github.com/CertyPro/certy-gh600-github-control-plane-lab)

## Two roles GitHub plays

| Role | Meaning |
| --- | --- |
| **Context source** | The agent **reads** GitHub artefacts as structured context for planning |
| **Control plane** | The agent **acts** through GitHub - it is steered by issues and produces PRs, comments and Actions runs |

## Artefacts the agent reads

- **Issues** - body, title, labels, assignees (often the task definition for a run).
- **Pull requests** - description, diff, review comments, status checks.
- **Comments** - human guidance and follow-up instructions.
- **Commits and diffs** - what changed and why.
- **Actions runs** - CI status, logs and results.

Treat issue bodies, labels and PR descriptions as **structured context** the planner uses.

## Driving an agent from an issue

```
issue opened/labelled -> agent reads issue as goal -> plans -> acts via tools
   -> opens PR / comments -> CI (Actions) runs -> agent reads result -> iterates
```

## Consistency and staleness

- GitHub state changes mid-run (new comment, label change, PR merged).
- **Re-read** state at decision points rather than trusting the first read.
- Handle stale context: detect that the world moved and re-plan if needed.

## Access

- Use a **scoped token** - start read-only, add write scopes only when the agent needs them.
- Least privilege: a triage agent that only reads should not hold write or admin scopes.

## One-line recap

GitHub is both **context** (read issues, PRs, diffs, Actions) and a **control plane** (act via issues, PRs, Actions). Re-read at decision points; scope the token tightly.
