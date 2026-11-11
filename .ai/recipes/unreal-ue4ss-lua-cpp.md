# Recipe: Unreal Engine 4 / 5 Modding with UE4SS (Lua / C++) & Pak Tools

## When to Use
Use this recipe when modding an **Unreal Engine 4 or 5** game (`<Game>/Binaries/Win64/*.exe` and `<Game>/Content/Paks/`).

## 1. Setup & Live Object Dumping with UE4SS
1. Install **RE-UE4SS** into `<GameDir>\Binaries\Win64\`.
2. In `UE4SS-settings.ini`, enable `GuiConsoleVisible = 1` during development and dump headers (`DumpCXXHeaders` / `DumpUHT`) so the AI can read exact Blueprint/C++ UObject property names and UFunction signatures from `CXXHeaderDump/`!

## 2. Recommended Lua Mod Structure (`Mods/<ModName>/`)
```text
Mods/<ModName>/
├── enabled.txt
└── Scripts/
    ├── main.lua          # RegisterHook / NotifyOnNewObject / RegisterKeyBind
    └── config.lua        # User-tunable mod settings
```

## 3. Core UE4SS Lua Patterns
```lua
-- Hook after PlayerController ClientRestart
RegisterHook("/Script/Engine.PlayerController:ClientRestart", function(Context)
    local pawn = Context:get():K2_GetPawn()
    if pawn:IsValid() then
        print(string.format("[MyMod] Player Pawn spawned: %s\n", pawn:GetFullName()))
    end
end)
```

## 4. Verification
- Check `<GameDir>\Binaries\Win64\UE4SS.log` after hot-reloading mods in-game (`Ctrl+R` in UE4SS console).
