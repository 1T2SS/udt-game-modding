# MCP_AND_TOOLS.md — Proactive Modding Environment & MCP Setup (`game-modding`)

> **AI Agent Instruction**: On Day-0 Bootstrap, check what reverse-engineering tools, SDKs, and MCP servers are installed on the user's machine. **If `ilspycmd` (CLI decompiler), BepInEx templates, or Blender MCP (for 3D mod assets) are missing, explain why they make modding 10x smoother and ask the user if you can install/set them up right now!** Record everything in [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md) so future mod projects already have the setup ready.

---

## 1. Proactive MCP Servers & Modding Tools to Check

| Tool / MCP Server | Purpose in `game-modding` | How to Check & Offer Setup |
| :--- | :--- | :--- |
| **`ilspycmd` (.NET CLI Decompiler)** | Essential for Unity/C# modding: lets AI agents list classes and decompile specific types from `Assembly-CSharp.dll` directly in the terminal without guessing! | Run `ilspycmd --version`. **If missing**, ask the user: *"Can I install `ilspycmd` (`dotnet tool install -g ilspycmd`) so I can inspect the game's DLL classes directly instead of guessing method names?"* |
| **Blender MCP** (`blender` MCP server) | Used whenever a mod adds or edits custom 3D models, weapons, armor, vehicles, or cosmetics. | Check if `blender` MCP is connected (`get_addon_status`). If the mod involves 3D assets and Blender MCP isn't set up, ask if you can configure Blender + Blender MCP for them! |
| **BepInEx .NET Project Templates** | Official `dotnet new` templates for BepInEx 5 (Mono) and BepInEx 6 (IL2CPP) plugins. | Check `dotnet new list bepinex`. If missing, offer to run `dotnet new install BepInEx.Templates::2.0.0-be.4`. |

---

## 2. Modding Environment Doctor Commands

Run these checks on Day 0 and save the results in [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md):

```powershell
# 1. Check .NET SDK & Global Tools (Unity / C# Modding)
dotnet --version
dotnet --list-sdks
ilspycmd --version 2>$null

# 2. Check Java 21 JDK (for Minecraft Fabric / NeoForge 1.20.5+ / 1.21+)
java -version 2>$null

# 3. Check Rust / C++ Toolchain (for Unreal / Native DLL Hooks)
cargo --version 2>$null
where.exe cl 2>$null

# 4. Check Blender (if modding 3D meshes)
Get-ChildItem "C:\Program Files\Blender Foundation\Blender*\blender.exe" -ErrorAction SilentlyContinue | Select-Object -ExpandProperty FullName
```

### One-Command Auto-Setup (Run with User Permission if Missing)
- **Install .NET SDK**: `winget install Microsoft.DotNet.SDK.9`
- **Install CLI Decompiler (`ilspycmd`)**: `dotnet tool install -g ilspycmd`
- **Install BepInEx Templates & NuGet Source**:
  ```powershell
  dotnet nuget add source https://nuget.bepinex.dev/v3/index.json -n BepInEx
  dotnet new install BepInEx.Templates::2.0.0-be.4 --nuget-source https://nuget.bepinex.dev/v3/index.json
  ```
- **Install Eclipse Temurin Java 21 (for Minecraft Modding)**: `winget install EclipseAdoptium.Temurin.21.JDK`

---

## 3. Save Verified Setup Info for Future Creations
Once verified:
1. Update [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md) with `TARGET_INSTALL_PATH` (the game directory), engine/runtime type, and installed tools (`ilspycmd`, `dotnet`, `blender`, etc.).
2. Log reusable discoveries (e.g., how a specific game engine packages its assemblies or assets) in Section 5 of [`.ai/MEMORY.md`](./MEMORY.md) so `scripts/harvest-learnings.ps1` can feed them back to the UDT Hub!
