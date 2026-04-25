---
name: "elastra-materialize"
description: "Materialize minimal valid slash-command setup for the current agent"
---
<!-- elastra:generated-skill:v1 -->

Use Elastra command routing for this workflow.

When invoked, Call the MCP tool elastra_execute_command with:
- input: "/elastra_materialize $ARGUMENTS"

If no arguments are provided, use a concise default request aligned with this command.
Return only the final answer.

Slash command validation and normalization contract:
- Trigger must start with "/".
- Reserved triggers (cannot be created/updated): /clear, /new, /diff, /implement, /usage, /models, /permissions, /history, /exit, /auth, /feedback, /skills, /run, /search, /memory, /gittree, /metrics, /elastra-metrics.
- Normalization removes `elastra_` and `elastra-` prefixes from intent tokens:
  - `/elastra_explain` -> `/explain`
  - `/elastra-explain` -> `/explain`
- MCP command execution uses POST `/v1/skills/execute` through ExecuteCommand.
- Engine-intercepted system commands: /new, /models, /model, /permissions, /usage, /feedback, /bug, /diff, /metrics, /elastra-metrics.

