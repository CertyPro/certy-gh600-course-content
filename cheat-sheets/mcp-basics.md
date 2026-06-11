# Cheat Sheet - MCP Basics

**Domain 2.0 (25%)** | Lessons `gh-agentic-mcp-intro`, `gh-agentic-mcp-dev`, `gh-agentic-mcp-transports` | Repo [mcp-server-lab](https://github.com/CertyPro/certy-gh600-mcp-server-lab)

## What MCP is

The **Model Context Protocol** is an open protocol that standardises how a host application (an agent, IDE or assistant) connects to external context and tools through MCP servers. One host runs one MCP client per server.

```
Host (agent/IDE)  --MCP client-->  MCP server  -->  tools, resources, prompts
```

During initialisation the server **advertises its capabilities** to the client.

## The three primitives (know the difference)

| Primitive | What it is | Side effects? | Who invokes/attaches |
| --- | --- | --- | --- |
| **Tool** | A callable action with a typed input schema | Yes - may change things | The model invokes it |
| **Resource** | Read-only context (file, record, query result) | No | The application or user attaches it |
| **Prompt** | A reusable, parameterised prompt template | No | The host / user selects it |

> Exam trap: a **tool acts**; a **resource is read-only context**. Do not swap them.

## Building a server

1. Register a tool with a **typed input schema**.
2. **Validate** the input against the schema.
3. Do the work; return a **structured result**.
4. Write clear **names and descriptions** - the model chooses tools from these.

## Transports

| Transport | Where the server runs | Best for |
| --- | --- | --- |
| **stdio** | Local subprocess launched by the host, over standard in/out | Local, single-user tools |
| **HTTP + SSE / streamable HTTP** | Remote service over HTTP, streamed messages | Shared or hosted servers |

Pick by where the server runs and who shares it.

## Execution context and least privilege

- A tool runs with: arguments, scope, credentials and environment.
- Grant only what the task needs. A read-only tool should not hold write credentials.
- Read secrets from the environment - never hard-code them.

## One-line recap

MCP = host/client/server; **tools act, resources read**; **stdio local, SSE/HTTP remote**; validate inputs and scope to least privilege.
