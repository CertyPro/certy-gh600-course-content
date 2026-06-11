# Chapter 04 - Evaluation, Debugging & Iteration

**Exam domain:** 4.0 (15%)
**Certy lessons:** `gh-agentic-eval-frameworks`, `gh-agentic-trace-debugging`
**Practice repo:** [certy-gh600-evaluation-debugging-lab](https://github.com/CertyPro/certy-gh600-evaluation-debugging-lab)

---

## Teaching goal

By the end of this chapter the learner can build an evaluation dataset, score runs with appropriate rubrics, read a trace to locate a failure, run evals in CI, and iterate on the agent with evidence rather than guesswork.

## Before you start

- Clone the evaluation-debugging-lab and run its sample eval suite.
- Keep the [evaluation-frameworks cheat sheet](../../cheat-sheets/evaluation-frameworks.md) open.
- Have a few failing runs ready so there is something real to debug.

## Running order

1. **Why evals (lesson `gh-agentic-eval-frameworks`).** You cannot improve what you cannot measure. An eval suite turns "it feels better" into a score you can track across changes.
2. **Build a dataset.** Collect representative tasks with expected outcomes. Cover happy path, edge cases and known failure cases. Keep it version-controlled alongside the agent.
3. **Choose scoring methods.** Match the method to the task:
   - **Exact-match / rule-based** - deterministic checks (did it open the PR, did the output match the schema). Cheap and reliable.
   - **Model-graded (LLM-as-judge)** - a model scores open-ended output against a rubric. Use for quality judgements that rules cannot capture; pin the rubric so scores are comparable.
4. **Traces (lesson `gh-agentic-trace-debugging`).** A trace is the ordered record of a run: each reasoning step, tool call, input, output and timing. Walk a real trace top to bottom.
5. **Debug from the trace.** Locate where the run diverged - a bad plan, a failing or misused tool call, a hallucinated result, or a validation gap that let a wrong result through. Distinguish a planning failure from an execution failure from a validation failure.
6. **Iterate.** Change one thing (a prompt, a tool description, a validation rule), re-run the eval, compare scores. Run the suite in CI so regressions are caught on every change.

## Key points to land

- An eval **dataset** plus a **rubric** plus a **score** is how you know whether a change helped.
- Use rule-based scoring where outcomes are deterministic; use model-graded scoring for open-ended quality, with a fixed rubric.
- A **trace** is your primary debugging tool - reasoning, tool calls and results in order.
- Classify failures: planning, execution or validation. The fix differs for each.
- Run evals in CI and track scores over time to catch regressions.

## Common mistakes

- No held-out dataset, so "improvements" are judged on the same example that was tuned on.
- Using model-graded scoring for everything, including things a simple rule could check deterministically.
- Reading only the final output and never the trace, so the root cause stays hidden.
- Changing several things at once, so you cannot tell which change moved the score.
- Treating a single passing run as proof - run the whole suite.

## Exam mapping

Domain 4.0 is 15% of the exam. Expect questions on building eval datasets, choosing scoring methods (exact-match vs rule-based vs model-graded), reading traces, classifying failure types, and running evals in CI to catch regressions.

## Wrap-up

Learners commit an eval suite and a wired-up trace to their agent. Chapter 05 scales it from one agent to many.
