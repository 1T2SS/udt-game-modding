# LIBRARY_RADAR.md — Game Modding Frameworks & Tooling Guide

> **Preset**: `game-modding`
> **Rule for AI Agents**: Always identify the target game's engine and runtime FIRST using [`.ai/RESEARCH_PLAYBOOK.md`](./RESEARCH_PLAYBOOK.md), then choose the matching framework below. Never guess internal game class or method names without inspecting the game's assemblies, dumps, or scripts first.

---

## 1. Engine & Mod Loader Decision Tree

| Target Game Engine / Runtime | How to Identify in Game Folder | Recommended Mod Framework | Matching Recipe |
| :--- | :--- | :--- | :--- |
| **Unity (Mono Runtime)** | Has `<Game>_Data/Managed/Assembly-CSharp.dll` and `MonoBleedingEdge/` | **BepInEx 5.4.x** + **HarmonyX** (C# Class Library) | [`.ai/recipes/unity-bepinex-harmony-mono.md`](./recipes/unity-bepinex-harmony-mono.md) |
| **Unity (IL2CPP Runtime)** | Has `GameAssembly.dll` and `<Game>_Data/il2cpp_data/` | **BepInEx 6 (Bleeding Edge IL2CPP)** or **MelonLoader v0.6+** + **HarmonyX** | [`.ai/recipes/unity-il2cpp-bepinex6-melonloader.md`](./recipes/unity-il2cpp-bepinex6-melonloader.md) |
| **Unreal Engine 4 / 5** | Has `<Game>/Binaries/Win64/*.exe` and `<Game>/Content/Paks/*.pak` or `.utoc`/`.ucas` | **UE4SS** (Lua / C++ runtime scripting & live UObject dumper) + `repak` / `retoc` | [`.ai/recipes/unreal-ue4ss-lua-cpp.md`](./recipes/unreal-ue4ss-lua-cpp.md) |
| **Minecraft (Java Edition)** | Minecraft Java Launcher / Modrinth / CurseForge | **Fabric** (lightweight, fast updates, Mixins) or **NeoForge** (large content mods) | [`.ai/recipes/minecraft-fabric-neoforge.md`](./recipes/minecraft-fabric-neoforge.md) |
| **Native C++ / Rust DLL Hook or Scripted Game (Lua / Redscript / Papyrus)** | Custom engine `.exe` or built-in `Mods/` Lua directory | **Reloaded-II**, **MinHook / safetyhook** (Rust/C++ proxy DLL), or native Lua API | See `.ai/RESEARCH_PLAYBOOK.md` |

---

## 2. Approved Modding Libraries & Tools Radar

- **Unity Modding**:
  - **BepInEx.Templates** (`dotnet new bepinex5plugin` / `bepinex6plugin`) + **HarmonyX** (`HarmonyPatch`, `HarmonyPrefix`, `HarmonyPostfix`, `HarmonyTranspiler`).
  - **`BepInEx.AssemblyPublicizer.MSBuild`**: Automatically publicizes private fields/methods of `Assembly-CSharp.dll` at compile time so you can access `player.privateField` directly with zero slow reflection (`Traverse`/`AccessTools`)!
  - **UnityExplorer (Sinai)**: In-game runtime object inspector & C# REPL for testing hooks live.
- **Decompilation & Inspection CLI Tools**:
  - **`ilspycmd`** (cross-platform CLI decompiler for .NET/Unity DLLs — lets AI agents decompile specific classes to stdout or `.ai/research/`!).
  - **`Il2CppDumper` / `Cpp2IL`** (automated by BepInEx 6 / MelonLoader into `BepInEx/interop/` or `MelonLoader/Il2CppAssemblies/`).
- **3D Custom Assets & Models**:
  - **Blender MCP** (`blender` MCP server) for creating/editing custom 3D meshes, weapons, cosmetics, and exporting `.glb`/`.fbx` for AssetBundles or pak replacement.

---

## 3. Banned / Dangerous Modding Anti-Patterns (DO NOT USE)

| Banned Pattern | Why It Breaks Mods | Use This Instead |
| :--- | :--- | :--- |
| **Guessing internal game class or method names from memory** | Fails to compile or crashes at runtime | Run `ilspycmd` on the game's DLL (or inspect UE4SS CXXHeaderDump) first! |
| **Hardcoding the user's personal Steam path (`C:\Program Files (x86)\Steam\...`) directly in committed source** | Breaks compilation for other modders or CI | Use a `<GameDir>` property in a local `Directory.Build.props.user` (gitignored) + commit `Directory.Build.props.user.example` |
| **Committing copyrighted game binaries (`Assembly-CSharp.dll`, `UnityEngine.dll`, `.pak` files) to GitHub** | Copyright violation & huge repo size | Reference DLLs directly from `$(GameDir)` or a gitignored `lib/` folder |
| **Returning `false` in every `HarmonyPrefix` unconditionally** | Skips original game method and breaks other mods | Prefer `HarmonyPostfix` or `HarmonyTranspiler` unless intentionally replacing method execution |
