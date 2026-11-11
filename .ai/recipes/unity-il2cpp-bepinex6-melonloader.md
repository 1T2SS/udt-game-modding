# Recipe: Unity (IL2CPP Runtime) Mod with BepInEx 6 or MelonLoader

## When to Use
Use this recipe when the target Unity game uses **IL2CPP** (`GameAssembly.dll` + `<Game>_Data/il2cpp_data/` exist instead of `Managed/Assembly-CSharp.dll`).

## 1. Prerequisite: Generate IL2CPP Interop Dummy DLLs
Before compiling, ensure either **BepInEx 6 (Unity.IL2CPP)** or **MelonLoader v0.6+** has been installed in the game folder and launched once so that dummy C# interop assemblies exist in:
- BepInEx 6: `$(GameDir)\BepInEx\interop\Assembly-CSharp.dll`
- MelonLoader: `$(GameDir)\MelonLoader\Il2CppAssemblies\Assembly-CSharp.dll`

## 2. Inspect Interop Classes with `ilspycmd`
```powershell
ilspycmd -l c "$GameDir\BepInEx\interop\Assembly-CSharp.dll" | Select-String "Player"
```

## 3. Crucial IL2CPP Rules for AI Agents
- **Target Framework**: IL2CPP BepInEx 6 / MelonLoader 0.6+ uses **`net6.0`**.
- **Custom MonoBehaviours**: In IL2CPP, any custom C# `MonoBehaviour` class you inject into Unity **must** register itself with `ClassInjector.RegisterTypeInIl2Cpp<MyCustomBehaviour>()` (from `Il2CppInterop.Runtime.Injection`) before calling `AddComponent<MyCustomBehaviour>()`!
- **Collections & Strings**: Note when fields use `Il2CppSystem.Collections.Generic.List<T>` vs `System.Collections.Generic.List<T>`.

## 4. Verification Command
- **Build & Deploy**: `dotnet build -c Release`
