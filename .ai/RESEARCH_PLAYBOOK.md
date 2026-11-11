# RESEARCH_PLAYBOOK.md — Decompile-First Game Modding Research Protocol

> **Preset**: `game-modding`
> **MANDATORY RULE**: Never write a Harmony patch, Mixin, or native detour hook until you have inspected the target game's actual classes, method signatures, and fields and recorded them in `.ai/research/`.

---

## Step 1: Locate & Fingerprint the Target Game

1. Check if `TARGET_INSTALL_PATH` is already recorded in [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md). If not, search common Steam/Epic/Xbox paths or ask the user for the game folder path:
   ```powershell
   Get-ChildItem "C:\Program Files (x86)\Steam\steamapps\common", "D:\SteamLibrary\steamapps\common", "E:\SteamLibrary\steamapps\common" -Directory -ErrorAction SilentlyContinue
   ```
2. Inspect the game directory to determine the exact engine and runtime:
   - **Unity Mono**: `<Game>_Data\Managed\Assembly-CSharp.dll` exists. Check `<Game>_Data\Managed\netstandard.dll` or `mscorlib.dll` to determine whether the target framework is `netstandard2.1`, `net472`, or `netstandard2.0`.
   - **Unity IL2CPP**: `GameAssembly.dll` exists at root. Check if `BepInEx\interop\` or `MelonLoader\Il2CppAssemblies\` has already generated dummy interop DLLs (run the game once with BepInEx 6 / MelonLoader installed if not yet generated).
   - **Unreal Engine**: `<Game>\Binaries\Win64\*.exe` and `<Game>\Content\Paks\` exist. Check UE4SS `CXXHeaderDump` or `UHTHeaderDump`.

---

## Step 2: Decompile & Search Target Classes via CLI (`ilspycmd`)

For Unity (Mono or IL2CPP interop DLLs) and .NET games, use `ilspycmd` (check/install via [`.ai/MCP_AND_TOOLS.md`](./MCP_AND_TOOLS.md)):

```powershell
# 1. List all types (classes/structs/enums) in Assembly-CSharp.dll matching a keyword:
ilspycmd -l c "$GameDir\<Game>_Data\Managed\Assembly-CSharp.dll" | Select-String -Pattern "Player|Inventory|Health|Weapon"

# 2. Decompile a specific class directly to inspect its exact methods and fields:
ilspycmd -t "Namespace.PlayerController" "$GameDir\<Game>_Data\Managed\Assembly-CSharp.dll" > .ai\research\PlayerController.cs
```

Always save decompiled reference snippets or notes into `.ai/research/` (gitignored if large, or summarized in `.ai/research/target-api-notes.md`) so you and future AI sessions know the exact method signatures, parameter types, and field names!

---

## Step 3: Verify Mod Loader Logs After Build

After building and copying the mod to the game folder, verify how to read the mod loader log file:
- **BepInEx**: `<GameDir>\BepInEx\LogOutput.log`
- **MelonLoader**: `<GameDir>\MelonLoader\Latest.log`
- **UE4SS**: `<GameDir>\Binaries\Win64\UE4SS.log`
- **Minecraft Fabric/NeoForge**: `run\logs\latest.log`
