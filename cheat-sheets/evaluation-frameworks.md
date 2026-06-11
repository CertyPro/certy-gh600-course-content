# Cheat Sheet - Evaluation Frameworks

**Domain 4.0 (15%)** | Lessons `gh-agentic-eval-frameworks`, `gh-agentic-trace-debugging` | Repo [evaluation-debugging-lab](https://github.com/CertyPro/certy-gh600-evaluation-debugging-lab)

## The eval triangle

```
dataset  +  rubric  +  score  =  knowing whether a change helped
```

## Building a dataset

- Representative tasks with **expected outcomes**.
- Cover happy path, edge cases and known failures.
- Version-control it next to the agent. Keep a held-out set you do not tune on.

## Scoring methods

| Method | How it scores | Use when |
| --- | --- | --- |
| **Exact-match / rule-based** | Deterministic checks (did it open the PR? does output match schema?) | Outcomes are deterministic - cheap and reliable |
| **Model-graded (LLM-as-judge)** | A model scores output against a fixed rubric | Open-ended quality that rules cannot capture |

Prefer rule-based where you can; reserve model-graded for genuine quality judgements, with a **pinned rubric** so scores compare.

## Traces

A **trace** is the ordered record of a run: each reasoning step, tool call, input, output and timing. It is your primary debugging tool.

## Classify the failure

| Symptom in the trace | Failure type | Fix area |
| --- | --- | --- |
| Wrong/incomplete plan | **Planning** | Prompt, planner logic, success criteria |
| Tool errored or misused | **Execution** | Tool, arguments, schema, context |
| Confident but false result | **Hallucination** | Grounding, validation |
| Wrong result passed through | **Validation gap** | Add/tighten validator |

## Iterate

- Change **one thing**, re-run the suite, compare scores.
- Run evals in **CI** to catch regressions on every change.
- Never judge on a single run - run the whole suite.

## One-line recap

Dataset + rubric + score; rule-based where deterministic, model-graded for quality; read the **trace** to classify the failure; iterate one change at a time in CI.
