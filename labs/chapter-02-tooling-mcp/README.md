# Chapter 02 - Tooling, MCP Servers & Execution Context

**Exam domain:** 2.0 (25% - the joint-largest domain)
**Certy lessons:** `gh-agentic-mcp-intro`, `gh-agentic-mcp-dev`, `gh-agentic-mcp-transports`
**Practice repo:** [certy-gh600-mcp-server-lab](https://github.com/CertyPro/certy-gh600-mcp-server-lab)

---

## Teaching goal

By the end of this chapter the learner can explain the Model Context Protocol, build a small MCP server with a tool and a resource, connect it to a host over both stdio and SSE, and reason about the execution context and permissions a tool runs with. This is one of the two heaviest domains, so spend time here.

## Before you start

- Clone the mcp-server-lab and confirm the runtime starts.
- Keep the [mcp-basics cheat sheet](../../cheat-sheets/mcp-basics.md) open.
- Have the [MCP docs](https://modelcontextprotocol.io) to hand for the spec details.

## Running order

1. **What MCP is (lesson `gh-agentic-mcp-intro`).** MCP is an open protocol that standardises how a host application (an agent, IDE or assistant) connects to external context and tools through MCP servers. Draw the host-client-server relationship: the host runs an MCP client per server; the server advertises its capabilities during initialisation.
2. **Tools vs resources vs prompts.** Land the distinction clearly because the exam tests it:
   - **Tool** - a callable action with a typed input schema; the model invokes it and it may have side effects (write a file, open a PR).
   - **Resource** - read-only context the host can attach to the model's context (a file, a record, a query result). The application or user typically chooses to attach it.
   - **Prompt** - a reusable, parameterised prompt template the server offers to the host.
3. **Build a server (lesson `gh-agentic-mcp-dev`).** Register a tool with a typed input schema, validate the input, do the work, return a structured result. Then expose a resource and show the host attaching it. Emphasise good tool descriptions - the model picks tools from their descriptions.
4. **Transports (lesson `gh-agentic-mcp-transports`).** Compare:
   - **stdio** - the host launches the server as a local subprocess and talks over standard input and output. Best for local, single-user tools.
   - **HTTP with SSE / streamable HTTP** - the server runs as a remote service; the host connects over HTTP and receives streamed messages. Best for shared or hosted servers.
   Configure both against the same server in the lab.
5. **Execution context and least privilege.** Define the context a tool runs with: the arguments, the scope, the credentials and the environment. Grant only what the task needs. A tool that only reads issues should not hold write credentials.

## Key points to land

- A **tool** acts (and may change things); a **resource** is read-only context. Confusing the two is the classic exam trap.
- The model chooses tools by their **names and descriptions** - write them carefully.
- **stdio** is for local subprocesses; **SSE / streamable HTTP** is for remote servers. Pick by where the server runs and who shares it.
- Validate every tool input against its schema before doing work.
- Scope credentials to the task. Least privilege is both a security and an exam point.

## Common mistakes

- Treating a resource as if it were a tool (or vice versa).
- Vague tool descriptions, so the model calls the wrong tool or none at all.
- Skipping input validation and trusting whatever the model passes.
- Hard-coding secrets into the server instead of reading them from the environment.
- Choosing a remote transport for a purely local tool, adding needless network surface.

## Exam mapping

Domain 2.0 is 25% of the exam. Expect several questions on the tool-vs-resource distinction, transport selection (stdio vs SSE), the host-client-server model, capability advertisement during initialisation, and least-privilege execution context.

## Wrap-up

Learners connect their Chapter 01 agent to the MCP server they built, so the agent now acts through a real tool. They will give it memory and GitHub context in Chapter 03.
