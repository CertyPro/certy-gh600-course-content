# Cheat Sheet - Agent Architectures

**Domain 1.0 (15%)** | Lessons `gh-agentic-reasoning-patterns`, `gh-agentic-transition-control` | Repo [agent-starter](https://github.com/CertyPro/certy-gh600-agent-starter)

## The agent loop

An agent is a loop around a model:

```
receive goal -> reason -> act (tool) -> observe -> decide: continue / validate / stop / hand back
```

## The three roles

| Role | Responsibility |
| --- | --- |
| **Planner** | Decompose the goal into ordered steps with explicit success criteria |
| **Executor** | Carry out a step, usually by calling a tool |
| **Validator** | Check the result against the success criteria before continuing |

## Reasoning patterns

| Pattern | What it does | Use when |
| --- | --- | --- |
| **ReAct** | Interleave reasoning and acting, one step at a time | The path is uncertain and must adapt to results |
| **Plan-and-execute** | Plan the whole sequence up front, then run it | The task is predictable; you want lower cost and clearer control |
| **Reflection** | The agent critiques its own output and retries | Output quality matters and a self-check improves it |

## Transition control (exam-critical)

- Define the condition for each transition: reason then act, act then validate, validate then continue or stop.
- Always set a **step budget** (max steps) and a **stop condition**.
- Handing back to a human is a valid transition, not a failure.

## Validation

- Success criteria belong in the plan, set before the work.
- Check for **correctness against the goal**, not just absence of error.
- No validation means no trust.

## Failure modes and guards

| Failure | Guard |
| --- | --- |
| Looping forever | Step budget + stop condition |
| Premature completion | Mandatory validation gate |
| Unbounded steps / cost | Cap steps and tokens |
| "Clean but wrong" result | Validate against success criteria, not just for errors |

## One-line recap

A trustworthy agent = planner + executor + **validator**, inside a loop with a stop condition and a step budget.
