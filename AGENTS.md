# AGENTS.md — Universal AI Agent Instructions (`game-modding`)

> **Preset**: `Universal Game Modding & Reverse-Engineering Template` (`game-modding`)
> **Summary**: AI-first preset for modding Unity (Mono/IL2CPP), Unreal Engine, Minecraft, and native/Lua games using a strict Decompile-First workflow.
> **Compatibility**: Antigravity (Gemini), Claude Code, Cursor, Windsurf, GitHub Copilot, Cline / Roo Code, OpenAI Codex, Aider, and all `AGENTS.md`-aware agents.

---

## 1. Mandatory First-Turn Startup Sequence

Whenever you begin a session in this repository, **before writing or modifying application code**, execute these steps in order:

1. **Check Project Initialization State**:
   - Read [`.ai/SPEC.md`](./.ai/SPEC.md) and [`.ai/ENVIRONMENT.md`](./.ai/ENVIRONMENT.md).
   - **If `status: UNINITIALIZED` in `.ai/SPEC.md`**: You are in a newly created project from the `game-modding` template. Immediately load and follow **[`.ai/BOOTSTRAP.md`](./.ai/BOOTSTRAP.md)** (the Day-0 Onboarding, Environment/MCP Doctor, Research & Scaffolding Protocol).
   - **If `status: INITIALIZED`**: Read [`.ai/MEMORY.md`](./.ai/MEMORY.md) and [`.ai/QC_REPORT.md`](./.ai/QC_REPORT.md) to resume from the exact architectural state, quality scorecard, and next steps left by the previous session or agent.

2. **Load Domain Intelligence (`.ai/`)**:
   - **[`.ai/LIBRARY_RADAR.md`](./.ai/LIBRARY_RADAR.md)** — Curated tech-stack decision tree, recommended high-performance libraries, and **explicitly banned/deprecated bloatware** for `game-modding`. Never suggest or install a library on the Banned list unless the user explicitly overrides it.
   - **[`.ai/MCP_AND_TOOLS.md`](./.ai/MCP_AND_TOOLS.md)** — Proactive **Environment & MCP Server Checklist**. Check which MCP servers (e.g., Blender MCP for 3D, Chrome DevTools MCP for web, decompilers for modding, Android Device Hub for mobile) and CLI tools are available. If a helpful MCP server or CLI tool is missing, **tell the user and ask if you can install/set it up for them**, then record the result in [`.ai/ENVIRONMENT.md`](./.ai/ENVIRONMENT.md).
   - **[`.ai/RESEARCH_PLAYBOOK.md`](./.ai/RESEARCH_PLAYBOOK.md)** — Domain-specific research protocol. Always verify current library versions, breaking API changes, or target game/platform schemas before coding, and save reusable findings in `.ai/research/`.
   - **[`.ai/QUALITY_CONTROL.md`](./.ai/QUALITY_CONTROL.md)** — Mandatory **Single Master Quality Control (QC) Sub-Agent Gate (`>= 8.5 / 10`)** executed at the end of every development round.

---

## 2. Core Vibe-Coding & Engineering Standards

- **Proactive Environment & MCP Setup**: Do not blindly assume compilers, SDKs, or MCP servers are missing or broken, and do not fail silently. Check [`.ai/ENVIRONMENT.md`](./.ai/ENVIRONMENT.md) first; run non-destructive doctor/version checks (`--version`); if a tool or MCP server (like Blender MCP in 3D game-dev, `uv` in Python, `cargo` in Rust, or `ilspycmd` in modding) would significantly improve the workflow and isn't configured yet, **proactively offer to set it up** and document the working setup in [`.ai/ENVIRONMENT.md`](./.ai/ENVIRONMENT.md).
- **Evidence Over Guesswork**: Never hallucinate package versions, CLI flags, or internal APIs. Follow [`.ai/RESEARCH_PLAYBOOK.md`](./.ai/RESEARCH_PLAYBOOK.md) to check live docs, MCP documentation servers, or local binary/assembly definitions first.
- **Modular, Agent-Friendly Code Structure**:
  - Keep source files focused and under **~300 lines** wherever practical so any AI agent can read and edit files cleanly without context truncation.
  - Separate domain logic, UI/presentation, configuration, and external integrations cleanly.
  - Never leave broken placeholder stubs (`TODO: implement later`) in critical paths unless explicitly requested.
- **Verify Every Change**: Every feature or fix must be validated using the build, lint, test, or runtime verification commands recorded in [`.ai/SPEC.md`](./.ai/SPEC.md).
- **Secret & Credential Hygiene**: Never hardcode API keys, tokens, or private paths in source files. Always use `.env` (gitignored) + `.env.example`.

---

## 3. Mandatory End-of-Round Gate: Single Master QC Sub-Agent (`>= 8.5 / 10`)

Whenever a project milestone or development round is completed and ready for review:

1. **Use ONE Master Quality Control Sub-Agent (Never Multiple Noisy Sub-Agents)**:
   - Follow **[`.ai/QUALITY_CONTROL.md`](./.ai/QUALITY_CONTROL.md)** to invoke **one** comprehensive Master QC Sub-Agent (`master-qc-director` — acting as a combined **AAA Creative/Art Director + Principal Staff Architect**):
     - **In Antigravity**: Call `define_subagent` / `invoke_subagent` for `master-qc-director` (with MCP tools enabled so it can inspect Blender MCP `look` renders, Chrome DevTools, or test outputs).
     - **In Claude Code**: Invoke the native `.claude/agents/master-qc-director.md` sub-agent.
     - **In Single-Agent IDEs (Cursor / Windsurf / Copilot / Cline)**: Execute a dedicated, zero-trust **Master QC Director Audit Pass** strictly following `.ai/QUALITY_CONTROL.md`.
2. **Strict `8.5 / 10` Floor Across All 5 Categories**:
   - The Master QC Sub-Agent grades all 5 domain categories in [`.ai/QUALITY_CONTROL.md`](./.ai/QUALITY_CONTROL.md) using a **Zero-Trust Deduction Rubric** (starting from `10.0` and deducting points for any missing visual/runtime evidence, rough models/UI, weak mechanics, or code smells) and writes the scorecard to **[`.ai/QC_REPORT.md`](./.ai/QC_REPORT.md)**.
   - **Pass Rule**: Both the **Overall Score** AND **every single category** must be **`>= 8.5 / 10.0`**.
3. **Auto-Refinement Loop (Up to 3 Rounds)**:
   - If **any category is `< 8.5 / 10`**, the round is **NOT** complete (`qc_status: REFINEMENT_REQUIRED`).
   - Immediately fix all flaws listed in [`.ai/QC_REPORT.md`](./.ai/QC_REPORT.md) and re-run the Master QC Sub-Agent check (up to **3 refinement rounds max**) before presenting the finished work to the user.

---

## 4. Continuous Cross-Agent Memory & Upstream Learning

This project is designed so the user can switch between AI agents at any time without losing context, AND so discoveries made here improve future projects:

1. **After completing a milestone or QC round**: Update [`.ai/SPEC.md`](./.ai/SPEC.md), [`.ai/QC_REPORT.md`](./.ai/QC_REPORT.md), and [`.ai/MEMORY.md`](./.ai/MEMORY.md).
2. **After verifying or fixing dev environment / MCP tools**: Update [`.ai/ENVIRONMENT.md`](./.ai/ENVIRONMENT.md).
3. **Give Future Creations Better Starting Info**: Whenever you discover a crucial library gotcha, a better setup command, or an MCP workflow trick, append it to Section 5 of [`.ai/MEMORY.md`](./.ai/MEMORY.md) (`Template & Environment Learnings`). The user can harvest these learnings back into their central `Universal-Development-Templates` Hub with one command (`scripts/harvest-learnings.ps1`).
