# Diagrams

Text and ASCII diagrams for the core GH-600 concepts. They are deliberately plain so they render anywhere and can be read aloud for accessibility.

---

## 1. The agent loop

How a single agent turns a goal into validated work.

```
                 +-----------------------------+
   goal  ----->  |           PLANNER           |
                 |  decompose into steps with  |
                 |  explicit success criteria  |
                 +--------------+--------------+
                                |
                                v
                 +-----------------------------+
            +--> |           EXECUTOR          |
            |    |  carry out the next step    |
            |    |  (usually a tool call)      |
            |    +--------------+--------------+
            |                   |
            |                   v
            |    +-----------------------------+
            |    |          OBSERVE            |
            |    |  read the tool result /     |
            |    |  intermediate state         |
            |    +--------------+--------------+
            |                   |
            |                   v
            |    +-----------------------------+
            |    |          VALIDATOR          |
            |    |  result meets criteria?     |
            |    +------+---------------+------+
            |           |               |
            |       pass|               |fail
            |           v               v
            |   +--------------+   +--------------+
            +---| more steps   |   | retry  /     |
        (budget | & budget     |   | hand back to |
         not    | remaining?   |   | a human      |
         spent) +------+-------+   +--------------+
                       |
                  no   | yes -> loop back to EXECUTOR
                       v
                +--------------+
                |    STOP      |
                | return result|
                +--------------+
```

Guards on the loop: a **step budget** and a **stop condition** prevent unbounded looping; the **validator** prevents premature or wrong completion.

---

## 2. A multi-agent pipeline (orchestrator + workers, with guardrails)

How an orchestrator drives workers over shared, locked state, gated by governance controls, in a GitHub-driven workflow.

```
   GitHub issue (the goal / context source)
            |
            v
   +-------------------+        input filter (validate, sanitise,
   |   INPUT FILTER    | <----- defend against prompt injection)
   +---------+---------+
             |
             v
   +-------------------+
   |   ORCHESTRATOR    |  decompose goal, dispatch, assemble result
   +----+----+----+----+
        |    |    |
        v    v    v
   +------+ +------+ +------+
   |WORKER| |WORKER| |WORKER|   specialised agents (each may call MCP tools)
   |  A   | |  B   | |  C   |
   +--+---+ +--+---+ +--+---+
      |        |        |
      +---+----+----+---+
          |  state lock |     only one writer at a time;
          v  (shared)   v     conflict policy resolves clashes
   +-------------------+
   |   SHARED STATE    |
   +---------+---------+
             |
             v
   +-------------------+        high-risk action? pause for
   |  APPROVAL GATE    | <----- human sign-off
   +---------+---------+
             |
             v
   +-------------------+        strip secrets, tokens, PII
   | OUTPUT REDACTION  | -----> before logging / returning
   +---------+---------+
             |
             v
   PR / comment / Actions run  ---->  AUDIT LOG (who, what, when,
   (GitHub as control plane)          authority, outcome - redacted)
```

Reading guide: untrusted input is filtered first; the orchestrator coordinates workers; shared state is protected by a **lock** with a stated **conflict policy**; high-risk actions pass through a **human approval gate**; output is **redacted** before it leaves; everything significant is written to an **audit log**.
