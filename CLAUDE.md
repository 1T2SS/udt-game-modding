# CLAUDE.md — Claude Code Entrypoint (`game-modding`)

This repository uses the **Universal Development Templates (UDT)** cross-agent protocol.

## Mandatory Startup & Quality Control Instructions
1. Read **[`AGENTS.md`](./AGENTS.md)** immediately — it is the single source of truth for all AI agents in this project.
2. Check **[`.ai/SPEC.md`](./.ai/SPEC.md)**:
   - If `status: UNINITIALIZED`, execute **[`.ai/BOOTSTRAP.md`](./.ai/BOOTSTRAP.md)** (Day-0 Onboarding, Environment/MCP Doctor, Research & Scaffolding).
   - If `status: INITIALIZED`, read **[`.ai/MEMORY.md`](./.ai/MEMORY.md)**, **[`.ai/ENVIRONMENT.md`](./.ai/ENVIRONMENT.md)**, and **[`.ai/QC_REPORT.md`](./.ai/QC_REPORT.md)** before making changes.
3. Consult **[`.ai/LIBRARY_RADAR.md`](./.ai/LIBRARY_RADAR.md)**, **[`.ai/MCP_AND_TOOLS.md`](./.ai/MCP_AND_TOOLS.md)**, and **[`.ai/RESEARCH_PLAYBOOK.md`](./.ai/RESEARCH_PLAYBOOK.md)** for domain-specific stack decisions, MCP server setup (such as Blender MCP, Chrome DevTools MCP, etc.), and research rules.
4. **End-of-Round Master QC Sub-Agent Gate (`>= 8.5 / 10`)**: When a development round is complete, invoke the single **`master-qc-director`** sub-agent (defined in [`.claude/agents/master-qc-director.md`](./.claude/agents/master-qc-director.md) and [`.ai/QUALITY_CONTROL.md`](./.ai/QUALITY_CONTROL.md)). If any category in [`.ai/QC_REPORT.md`](./.ai/QC_REPORT.md) scores `< 8.5 / 10`, refine the project and re-verify (up to 3 rounds) before finishing.
