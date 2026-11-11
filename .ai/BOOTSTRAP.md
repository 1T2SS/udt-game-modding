# BOOTSTRAP.md — Day-0 Onboarding, Environment/MCP Doctor & Scaffolding Protocol

> **Preset**: `Universal Game Modding & Reverse-Engineering Template` (`game-modding`)
> **Trigger Condition**: Execute this protocol automatically whenever `status: UNINITIALIZED` in [`.ai/SPEC.md`](./SPEC.md).

---

## Phase 1: Understand the Idea & Recommend the Best Stack

1. Read the user's initial prompt carefully, then read [`.ai/LIBRARY_RADAR.md`](./LIBRARY_RADAR.md) and [`.ai/MCP_AND_TOOLS.md`](./MCP_AND_TOOLS.md).
2. If the user's first prompt leaves key architectural choices open, ask **at most 3–4 concise, high-impact questions** (with your recommended option listed first based on `.ai/LIBRARY_RADAR.md`):
   - **Core Stack / Engine / Runtime** (e.g., which recipe from `.ai/recipes/` fits best).
   - **Scope & Key Features for v1** (what "working v1" looks like).
   - **Special Integrations or Asset Pipelines** (e.g., 3D modeling via **Blender MCP** in `game-dev`, target game & runtime in `game-modding`, target browsers in `browser-extension`, local vs cloud models in `ai-and-agents`).

---

## Phase 2: Proactive Environment & MCP Doctor (Check & Offer to Set Up!)

Before scaffolding or writing code, **check what the project needs vs. what is currently available** on the user's machine and in your agent environment:

1. **Inspect [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md) & [`.ai/MCP_AND_TOOLS.md`](./MCP_AND_TOOLS.md)**:
   - See if a machine profile was already carried over from the template hub.
2. **Check Available MCP Servers & Agent Capabilities**:
   - Inspect your active MCP tools/skills against the domain recommendations in [`.ai/MCP_AND_TOOLS.md`](./MCP_AND_TOOLS.md) (for example: **Blender MCP** when doing 3D modeling/assets in `game-dev` or `game-modding`; **Chrome DevTools MCP** in `web-app` or `browser-extension`; **Android Device Hub / CLI** in `mobile-app`; **Gemini API Docs / Developer Knowledge MCP** in `ai-and-agents`).
   - **If a recommended MCP server is available**: Tell the user you detected it and how you'll use it (e.g., *"I see Blender MCP is connected — I can generate and inspect 3D models directly in Blender for your game"*).
   - **If a recommended MCP server is NOT connected/installed**: Proactively mention it and ask the user if they want you to help set it up or configure it now!
3. **Run Non-Destructive CLI & SDK Checks**:
   - Run lightweight version checks (`cargo --version`, `uv --version`, `bun --version`, `dotnet --version`, `godot --version`, `ilspycmd --version`, etc.) for the chosen stack.
   - **If a required runtime, compiler, or CLI tool is missing**: Do NOT fail silently or fall back to an inferior stack. Explain what is missing, provide the exact install command (`winget`, `scoop`, `cargo install`, `uv tool install`, etc.), and **ask if you can install/configure it for them right now**.
4. **Record Verified Environment State**:
   - Update [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md) with exact versions, paths, and active MCP servers so future turns (and future projects harvested via `harvest-learnings.ps1`) start with complete knowledge of the machine.

---

## Phase 3:Targeted Pre-Coding Research

Follow [`.ai/RESEARCH_PLAYBOOK.md`](./RESEARCH_PLAYBOOK.md):
- Verify the latest stable versions and CLI scaffolding flags for the chosen stack.
- Never rely on outdated training data when official docs, MCP documentation tools, or package registries (`npm view`, `cargo search`, `uv`, etc.) can be checked in seconds.
- Save any important discoveries (API schemas, target game assembly signatures, engine version notes) in `.ai/research/`.

---

## Phase 4: Scaffold, Clean Up & Lock Spec

1. **Apply the Chosen Recipe**:
   - Open the matching recipe in `.ai/recipes/` for the chosen stack.
   - Run the official CLI initializer or create the clean directory layout specified in the recipe.
2. **Clean Up Unused Recipes**:
   - Once the project's stack is chosen and initialized, delete the unused stack recipes from `.ai/recipes/` (keep only the recipe(s) relevant to this project) so future AI sessions aren't distracted by irrelevant stacks.
3. **Lock [`.ai/SPEC.md`](./SPEC.md) & [`.ai/MEMORY.md`](./MEMORY.md)**:
   - Change `status: UNINITIALIZED` to `status: INITIALIZED` in `.ai/SPEC.md`.
   - Fill in the chosen stack, directory map, exact build/dev/test commands, and initial milestone plan.
   - Log the bootstrap completion and any environment/setup lessons in `.ai/MEMORY.md` (including Section 5 for upstream template learnings).
4. **Verify**:
   - Run the project's build, check, or dev smoke test to prove the scaffold works out of the box before starting feature work.
