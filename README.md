# GH-600 GitHub Agentic AI Developer - Course Content

> Build, supervise, and govern autonomous agents in GitHub-driven delivery.

This is the public teaching hub for the **GH-600 GitHub Agentic AI Developer** course by [Certy](https://certy.pro), built and maintained by [Coded Vision Design](https://github.com/CertyPro). It contains the lesson map, exam objectives, instructor lab walkthroughs, cheat sheets, practice questions, a glossary, diagrams and the capstone brief.

The free written course and the mock exam live at **[certy.pro](https://certy.pro)**. The hands-on practice repositories live under the [CertyPro organisation](https://github.com/CertyPro).

---

## The repo set

The course is delivered across one content hub (this repo) and seven hands-on lab repositories. Each lab maps to an exam domain.

| Repo | Purpose | Domain |
| --- | --- | --- |
| [certy-gh600-course-content](https://github.com/CertyPro/certy-gh600-course-content) | This hub - objectives, lesson map, cheat sheets, labs, glossary, capstone | All |
| [certy-gh600-agent-starter](https://github.com/CertyPro/certy-gh600-agent-starter) | Minimal agent scaffold (planner, executor, validator) you extend throughout the course | 1.0 Agent Architecture, Planning & Validation |
| [certy-gh600-mcp-server-lab](https://github.com/CertyPro/certy-gh600-mcp-server-lab) | Build and connect Model Context Protocol servers, tools and resources over stdio and SSE | 2.0 Tooling, MCP Servers & Execution Context |
| [certy-gh600-memory-state-lab](https://github.com/CertyPro/certy-gh600-memory-state-lab) | Short-term, episodic and semantic memory; state serialisation and checkpoints | 3.0 Memory, State & GitHub Context |
| [certy-gh600-github-control-plane-lab](https://github.com/CertyPro/certy-gh600-github-control-plane-lab) | Use GitHub issues, PRs, Actions and the API as the agent's control plane and context source | 3.0 Memory, State & GitHub Context |
| [certy-gh600-evaluation-debugging-lab](https://github.com/CertyPro/certy-gh600-evaluation-debugging-lab) | Eval datasets, rubrics, trace inspection and the iteration loop | 4.0 Evaluation, Debugging & Iteration |
| [certy-gh600-multi-agent-orchestration-lab](https://github.com/CertyPro/certy-gh600-multi-agent-orchestration-lab) | Orchestrator and worker agents, handoffs, state locking and conflict resolution | 5.0 Multi-Agent Systems & Orchestration |
| [certy-gh600-governance-guardrails-lab](https://github.com/CertyPro/certy-gh600-governance-guardrails-lab) | Input safeguards, output redaction, approval gates and audit logs | 6.0 Governance, Guardrails & Compliance |

---

## How to use this course

1. **Read the free course at [certy.pro](https://certy.pro).** Work through the 15 lessons in order; they map to the six exam domains.
2. **Clone the matching lab repo** for each domain and complete the exercises. Use the instructor walkthroughs in [`labs/`](./labs) as a guide.
3. **Keep the [cheat sheets](./cheat-sheets) open** while you work - they distil the exam-critical points per domain.
4. **Self-test** with the [practice questions](./practice-questions) here, then sit the full **mock exam at [certy.pro](https://certy.pro)**.
5. **Finish with the [capstone](./challenge-project)** - extend the agent-starter into a supervised, governed agent that touches every domain.
6. **Book the official GH-600 exam** when your mock-exam scores are consistently above the pass mark.

---

## Contents

- [`README.md`](./README.md) - this overview
- [`exam-objectives.md`](./exam-objectives.md) - the six domains, weights, skills and matching lessons and labs
- [`lesson-map.md`](./lesson-map.md) - the 15 Certy lessons mapped to chapters and repos
- [`video-roadmap.md`](./video-roadmap.md) - planned video walkthroughs, one per domain
- [`labs/`](./labs) - instructor walkthrough notes for the six chapters
- [`cheat-sheets/`](./cheat-sheets) - one revision sheet per domain topic
- [`practice-questions/`](./practice-questions) - sample MCQs and a pointer to the mock exam
- [`glossary/`](./glossary) - key agentic-AI, MCP and GitHub terms
- [`diagrams/`](./diagrams) - ASCII diagrams of the agent loop and a multi-agent pipeline
- [`resources/`](./resources) - official cert, MCP and GitHub links plus all sibling repos
- [`challenge-project/`](./challenge-project) - the GH-600 capstone brief
- [`exam-objectives.md`](./exam-objectives.md), [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md), [`LICENSE`](./LICENSE), [`LICENSE-CONTENT.md`](./LICENSE-CONTENT.md)

---

## Exam at a glance

| Domain | Weight |
| --- | --- |
| 1.0 Agent Architecture, Planning & Validation | 15% |
| 2.0 Tooling, MCP Servers & Execution Context | 25% |
| 3.0 Memory, State & GitHub Context | 25% |
| 4.0 Evaluation, Debugging & Iteration | 15% |
| 5.0 Multi-Agent Systems & Orchestration | 10% |
| 6.0 Governance, Guardrails & Compliance | 10% |

See [`exam-objectives.md`](./exam-objectives.md) for the full skill breakdown per domain.

---

## Licensing

- **Code** in this repository and the sibling labs is licensed under the [MIT licence](./LICENSE).
- **Prose** (lessons, walkthroughs, cheat sheets, diagrams and questions) is licensed under [CC-BY-4.0](./LICENSE-CONTENT.md).

Attribution: Certy / Coded Vision Design. See [`LICENSE-CONTENT.md`](./LICENSE-CONTENT.md) for details.

---

Maintained by [Coded Vision Design](https://github.com/CertyPro) for [Certy](https://certy.pro). Contributions welcome - please read the [Code of Conduct](./CODE_OF_CONDUCT.md) first.
