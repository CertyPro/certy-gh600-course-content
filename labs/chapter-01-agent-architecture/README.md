# Chapter 01 - Agent Architecture, Planning & Validation

**Exam domain:** 1.0 (15%)
**Certy lessons:** `gh-agentic-reasoning-patterns`, `gh-agentic-transition-control`
**Practice repo:** [certy-gh600-agent-starter](https://github.com/CertyPro/certy-gh600-agent-starter)

---

## Teaching goal

By the end of this chapter the learner can explain the agent loop, name the planner, executor and validator roles, and reason about when an agent should keep going, validate, stop or hand back to a human. They leave with a working agent-starter they will extend for the rest of the course.

## Before you start

- Clone the agent-starter and run its tests so everyone starts green.
- Have the [agent-architectures cheat sheet](../../cheat-sheets/agent-architectures.md) open.
- Sketch the agent loop on a whiteboard before opening any code (see [`diagrams/`](../../diagrams)).

## Running order

1. **The agent loop (lesson `gh-agentic-reasoning-patterns`).** Walk the loop end to end: receive goal, reason about the next step, act (call a tool), observe the result, decide whether to continue. Stress that an agent is a loop around a model, not a single call.
2. **The three roles.** Map planner (decompose the goal into ordered steps with success criteria), executor (carry out a step, usually via a tool call), validator (check the result against the success criteria before moving on). In the starter these are separate functions - point at each one.
3. **Reasoning patterns.** Contrast ReAct (interleave reasoning and acting, one step at a time) with plan-and-execute (plan the whole sequence up front, then run it) and reflection (the agent critiques its own output and retries). Note the trade-off: ReAct adapts to surprises; plan-and-execute is cheaper and more predictable.
4. **Transition control (lesson `gh-agentic-transition-control`).** This is the exam-critical part. Decide the conditions for each transition: reason then act, act then validate, validate then continue or stop. Add a step budget and a stop condition so the loop cannot run forever.
5. **Validation in practice.** Show a validator rejecting a tool result and forcing a retry or a hand-back. Make the success criteria explicit and machine-checkable, not vibes.

## Key points to land

- The validator is what separates an agent from a hopeful prompt. No validation means no trust.
- Every loop needs a stop condition and a step budget. State them explicitly.
- Success criteria belong in the plan, set before the work, not judged after the fact.
- Handing back to a human is a valid, often correct, transition - not a failure.

## Common mistakes

- **No step budget** - the agent loops until it runs out of tokens or money. Always cap it.
- **Premature completion** - the agent declares success without validating. Force a validation gate.
- **Validation that only checks for an error, not for correctness** - a tool can return cleanly and still be wrong for the goal.
- **Blurring planner and executor** - mixing planning into the action step makes runs hard to debug. Keep them separate.

## Exam mapping

This chapter covers all of domain 1.0: agent loop and roles, reasoning patterns (ReAct, plan-and-execute, reflection), planning with success criteria, transition and stop control, and validation of intermediate state. Expect questions that give a scenario and ask which transition or which guard is appropriate.

## Wrap-up

Learners should commit their extended agent-starter with a validator and a step budget in place. They will build tools onto this in Chapter 02.
