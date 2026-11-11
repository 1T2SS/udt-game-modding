# QUALITY_CONTROL.md — Master Quality Control Sub-Agent Protocol (`game-modding`)

> **Preset**: `game-modding`
> **QC Persona**: **Master Modding Architect, Reverse-Engineering Lead & Game Balance/Art Director** (`master-qc-director`)
> **Mandatory Rule**: Use **ONE** Master Quality Control Sub-Agent at the end of each development round. Never spawn multiple separate review sub-agents.
> **Pass Threshold**: Overall Average **`>= 8.5 / 10.0`** AND **every individual category `>= 8.5 / 10.0`**.

---

## 1. How to Invoke the Single Master QC Check

When a modding round (new Harmony patches, UE4SS scripts, Mixins, or custom 3D mod assets) is complete:
- **Antigravity**: Define/invoke the single `master-qc-director` sub-agent (`EnableWriteTools: true`, `EnableMCPTools: true`) to audit decompiled hook accuracy, build output, and any custom 3D meshes (via Blender MCP `look`), writing the scorecard to `.ai/QC_REPORT.md`.
- **Claude Code**: Invoke `.claude/agents/master-qc-director.md`.
- **Cursor / Windsurf / Copilot / Cline**: Execute a dedicated **Master QC Director Audit Pass** using the rubric below and write `.ai/QC_REPORT.md`.

---

## 2. The 5-Pillar Zero-Trust Deduction Rubric (Starts at `10.0` Per Category)

### Category 1: Decompiled API Accuracy & Hook Safety (`>= 8.5 / 10`)
- **`-4.0 pts` (Automatic Fail)**: Guessing internal game class, method, or field names without verifying them against `ilspycmd` decompiled output, UE4SS headers, or `.ai/research/` notes!
- **`-2.0 pts`**: Using destructive `HarmonyPrefix` (`return false;`) or `@Redirect` when a non-destructive `HarmonyPostfix`, `HarmonyTranspiler`, or `MixinExtras` (`@WrapOperation` / `@ModifyReturnValue`) would preserve compatibility with other mods.
- **`-1.5 pts`**: Missing null/validity checks on hooked game instances (e.g., assuming `Player.Instance` is non-null during loading screens).

### Category 2: In-Game Mechanics, Balance & Visual / 3D Asset Quality (`>= 8.5 / 10`)
- **`-2.0 pts`**: If custom 3D models/weapons/cosmetics are included and were NOT verified in **Blender MCP (`look` / `get_scene_info`)** for scale, rig/bone alignment, and material assignment.
- **`-1.5 pts`**: Janky in-game integration (UI/HUD elements clashing with the vanilla game's art style, jarring audio/visual transitions, or unbalanced mechanics).

### Category 3: Code Architecture & Zero-Reflection Performance (`>= 8.5 / 10`)
- **`-2.0 pts`**: Running slow reflection (`AccessTools.Field`, `GetComponent`, `FindObjectsOfType`) inside per-frame `Update()` / `LateUpdate()` hooks instead of caching or using `BepInEx.AssemblyPublicizer`.
- **`-1.5 pts`**: Committing hardcoded personal Steam/game paths (`C:\Program Files...`) or copyrighted game DLLs instead of using gitignored `Directory.Build.props.user`.

### Category 4: Features, Mod Configurability & Completeness (`>= 8.5 / 10`)
- **`-2.0 pts`**: Hardcoding magic numbers (keybinds, multipliers, toggles) instead of exposing them via `ConfigEntry<T>` (BepInEx), MelonPreferences, ModMenu, or `config.lua`.
- **`-1.5 pts`**: Incomplete mod lifecycle handling (e.g., failing to clean up injected objects or event listeners on scene unload).

### Category 5: Build, Auto-Deploy & Log Cleanliness (`>= 8.5 / 10`)
- **`-3.0 pts` (Automatic)**: `dotnet build` / `./gradlew build` fails or emits unresolved reference errors.
- **`-1.5 pts`**: Missing structured mod logging (`Logger.LogInfo` / `LogError`) or missing automated post-build copy target to the game's mod folder.

---

## 3. Auto-Refinement Protocol (Up to 3 Rounds)
If any category scores `< 8.5 / 10`, `master-qc-director` sets `qc_status: REFINEMENT_REQUIRED` in [`.ai/QC_REPORT.md`](./QC_REPORT.md). The main agent must fix all listed deductions and re-run `master-qc-director` (up to 3 rounds max) before completing the round.
