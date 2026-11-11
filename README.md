# Universal Game Modding & Reverse-Engineering Template (`udt-game-modding`)

> **AI-First Vibe Coding Preset** for modding **Unity (Mono & IL2CPP via BepInEx / HarmonyX / MelonLoader)**, **Unreal Engine 4/5 (UE4SS Lua/C++)**, **Minecraft (Fabric / NeoForge)**, and **Lua / Native C++ / Rust** games.
> Built around a strict **Decompile-First Research Protocol** and proactive tool/MCP setup (`ilspycmd`, BepInEx templates, Blender MCP for custom 3D meshes) so AI agents never guess internal game classes!

---

## Quick Start (30 Seconds)

### Option A: From GitHub
1. Click **"Use this template" → "Create a new repository"** on GitHub.
2. Clone your new repo and open it in any AI coding agent.
3. Tell the AI which game you are modding (and optionally its install folder path) and what your mod should do!

### Option B: From Local UDT Hub
```powershell
.\scripts\new-project.ps1 -Preset game-modding -Target "E:\Projects\MyGameMod" -InitGit
```

---

## Why This Preset Is a Game-Changer for Modding
Without this template, AI agents try to guess internal game method names from memory and produce broken Harmony patches. This preset enforces:
1. **Engine & Runtime Auto-Detection**: Inspects the game folder to identify Unity Mono vs. Unity IL2CPP vs. Unreal vs. Scripted/Native.
2. **CLI Decompilation Setup (`ilspycmd`)**: Checks if you have CLI decompilation tools and **Blender MCP** (for custom 3D weapon/character/item meshes) installed — offering to set them up automatically if missing.
3. **One-Command Build & Deploy to Game Folder**: Configures post-build targets so compiling immediately drops your `.dll` / `.pak` / script into the game's `Mods` or `BepInEx/plugins` folder.
