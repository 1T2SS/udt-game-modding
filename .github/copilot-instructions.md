# GitHub Copilot Instructions — Universal Development Template (`game-modding`)

This project uses the **Universal Development Templates (UDT)** `.ai/` brain system.

1. Read [`AGENTS.md`](../AGENTS.md) at the repository root for the mandatory workflow.
2. Check [`.ai/SPEC.md`](../.ai/SPEC.md). When `status: UNINITIALIZED`, follow [`.ai/BOOTSTRAP.md`](../.ai/BOOTSTRAP.md) to help the user choose a stack from [`.ai/LIBRARY_RADAR.md`](../.ai/LIBRARY_RADAR.md), verify/set up CLI tools and MCP servers via [`.ai/MCP_AND_TOOLS.md`](../.ai/MCP_AND_TOOLS.md), and scaffold the project.
3. Never use libraries listed as Banned/Avoided in [`.ai/LIBRARY_RADAR.md`](../.ai/LIBRARY_RADAR.md).
4. At the end of every development round, follow [`.ai/QUALITY_CONTROL.md`](../.ai/QUALITY_CONTROL.md) and update [`.ai/QC_REPORT.md`](../.ai/QC_REPORT.md) — every category must score `>= 8.5 / 10` (auto-refine up to 3 rounds if any score is `< 8.5`).
5. Keep [`.ai/SPEC.md`](../.ai/SPEC.md), [`.ai/ENVIRONMENT.md`](../.ai/ENVIRONMENT.md), [`.ai/QC_REPORT.md`](../.ai/QC_REPORT.md), and [`.ai/MEMORY.md`](../.ai/MEMORY.md) updated as the architecture evolves.
