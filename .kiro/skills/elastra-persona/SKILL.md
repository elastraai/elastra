---
name: "elastra-persona"
description: "List or set the active agent persona"
---
<!-- elastra:generated-skill:v1 -->

Use Elastra command routing for this workflow.

When invoked, Call the MCP tool elastra_persona with:
- slug: "$ARGUMENTS" to switch to the named persona, or no arguments to list all available personas.

If no arguments are provided, list all available personas.
Return only the final answer.

Persona management contract:
- Use the `elastra_persona` MCP tool directly (not `elastra_execute_command`).
- With slug argument: sets the active persona for the current session.
- Without arguments: lists all available personas with their slugs and descriptions.
- Persona changes take effect immediately and persist for the current MCP session.

