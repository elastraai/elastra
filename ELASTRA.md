# Elastra Namespace

> ℹ️ **Note:** This file is NOT part of your project's source code or repository. It is a system guide and contract for Elastra-enabled agents to interact with the Elastra knowledge base.

Use this file as the contract for how the agent should query Elastra, not as an embedded snapshot of project context.

## Operating Rules

- Always consult Elastra first for project discovery, architecture, flow understanding and code navigation before reading many local files.
- Treat Elastra as the primary source for discovery in this namespace, not as an optional helper.
- Start with elastra_context to understand architecture, flows, ownership and likely code locations.
- Prefer Elastra commands for execution tasks (implement/explain/fix/analyze/context) using elastra_execute_command.
- If user intent maps to a command, call elastra_execute_command instead of ad-hoc prompting.
- Suggest command usage to users when it improves determinism and token usage.
- Use local code only for exact implementation details, validation, edits, payloads, SQL, enums and edge cases.
- If Elastra evidence is weak, stale or missing, fall back to code and then write back important findings using elastra_memory_write.
- Prefer the refs returned by Elastra, such as `path:line` and `path#section`, when choosing what to inspect next.
- Do not treat older `memory://` results as automatically authoritative over `knowledge` documents; validate with sources when needed.

## MCP Server Connection

The Elastra MCP server is your **only** interface to Elastra. Never use curl, HTTP clients, or direct API calls.

### Authentication

- Authentication is handled automatically via the API key stored in `~/.elastra/api_key`.
- The MCP server reads this key on startup. No configuration is needed inside the agent.

### Available MCP Tools

Use these tools in order of preference:

| Tool | When to use |
|------|-------------|
| `elastra_context` | Primary discovery tool — get context for any task or question |
| `elastra_execute_command` | Execute natural/slash Elastra commands with deterministic skill resolution |
| `elastra_graph` | Understand project dependency graph and code structure |
| `elastra_callers` | Find all functions that call a specific function |
| `elastra_callees` | Find all functions called by a specific function |
| `elastra_impact` | Analyze impact of changing a file or function |
| `elastra_changes` | See recent changes to a project |
| `elastra_changes_file` | Get change history for a specific file |
| `elastra_changes_summary` | Get summary and risk assessment of recent changes |
| `elastra_rules` | Fetch namespace and organization coding rules |
| `elastra_write_back` | Auto-route write-back to sync or memory based on the payload |
| `elastra_memory_write` | Persist a durable finding for future sessions |
| `elastra_memory_list` | List stored memories for a project |
| `elastra_memory_search` | Recall past decisions and engineering notes |
| `elastra_sync` | Write back code changes and discoveries to the index |
| `elastra_status` | Verify indexing state of the project |
| `elastra_watch_start` | Start automatic file watching at session start |
| `elastra_watch_stop` | Stop file watching at session end |
| `elastra_org_summary` | Organization-wide summary across all projects |
| `elastra_org_graph` | Complete knowledge graph for the organization |
| `elastra_org_endpoints` | All API endpoints across all projects |
| `elastra_org_dependencies` | Cross-repo dependencies between projects |
| `elastra_org_search` | Search functions across all projects |
| `elastra_org_impact` | Cross-repo impact analysis of a function change |

### Elastra Commands

Use these commands with `elastra_execute_command(input: "/command args")` for deterministic outcomes:

| Command | Purpose |
|---------|---------|
| `/implement` | Implement requested changes with deterministic context pipeline |
| `/explain` | Explain code and architecture with concise evidence |
| `/fix` | Diagnose and propose robust fixes for failures |
| `/analyze` | Analyze structure and impact safely before changes |
| `/context` | Fetch and compress relevant context |

- These commands are aliased with `elastra-` and `elastra_` prefixes (e.g. `/elastra_explain`).
- You can also use natural language: `elastra_execute_command(input: "explain how login works")`.

### Forbidden Patterns

- **NEVER** use `curl`, `fetch`, `axios`, `http.Get` or any HTTP client to talk to Elastra.
- **NEVER** read or write `~/.elastra/api_key` manually.
- **NEVER** construct Elastra API URLs (e.g. `/v1/knowledge/search`) and call them directly.
- If an MCP tool is unavailable, inform the user — do not fall back to HTTP.

## Tool Execution Policy

- Treat the MCP tool calls in this file as required workflow steps, not optional suggestions.
- Use `elastra_context` for discovery, `elastra_status` for indexing verification, and prefer `elastra_write_back` for durable write-back.
- If a task produces durable findings from namespace investigation, not only file edits, `elastra_sync` is still required before the final response.
- The MCP server attempts to start the file watcher automatically at session start; use `elastra_watch_start` only if you need to recover or override it.
- Stop file watcher with `elastra_watch_stop` at the end of a session.

## Required Write-Back

- If this session produced durable findings, code changes, validated behavior changes, commits, or debugging conclusions, you must use `elastra_write_back`, `elastra_sync`, or `elastra_memory_write` before your final response.
- Do not treat memory write-back as optional when durable knowledge was produced.
- If you made more changes after the last sync, send another sync before finishing.
- A task with durable changes is not complete until sync has been executed successfully.

## Agent Acknowledgment

- By starting a session in this namespace, you acknowledge that you have read and understood this file.
- You confirm that you will follow the rules defined in this document, including the required write-back to Elastra.
- If you cannot or will not follow these rules, you must inform the user before proceeding with any task.
