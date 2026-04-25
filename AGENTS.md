<!-- elastra:bootstrap:v1 -->
# Elastra Bootstrap

> ⚠️ **MANDATORY — Read before acting on any task.**

Your **very first action on every task** MUST be to call `elastra_context`. No exceptions.

Do NOT grep, glob, view, or read local files as a first step. Do NOT assume you know the codebase from memory.

```
elastra_context(query: "<task description>")
```

After discovery, use local files only for exact edits, validation, SQL, enums, and edge cases.

Read `ELASTRA.md` as the mandatory namespace contract for this project.
Before your final response, if you produced durable knowledge or code changes, you must use the elastra_sync or elastra_memory_write MCP tools.
<!-- /elastra:bootstrap:v1 -->

