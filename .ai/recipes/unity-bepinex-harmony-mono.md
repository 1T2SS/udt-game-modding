# Recipe: Unity (Mono Runtime) Mod with BepInEx 5 + HarmonyX

## When to Use
Use this recipe when the target Unity game has `<Game>_Data/Managed/Assembly-CSharp.dll` (Mono runtime).

## 1. Project Setup (`ModName.csproj` + `Directory.Build.props.user`)

Create `Directory.Build.props.user.example` (committed) and `Directory.Build.props.user` (gitignored) holding the local game path:
```xml
<Project>
  <PropertyGroup>
    <GameDir>C:\Program Files (x86)\Steam\steamapps\common\YourGameName</GameDir>
  </PropertyGroup>
</Project>
```

Configure the `.csproj` with the BepInEx NuGet feed, `BepInEx.AssemblyPublicizer.MSBuild` (so private game fields/methods can be accessed with zero reflection), and an automatic post-build copy into `$(GameDir)\BepInEx\plugins\`:
```xml
<Project Sdk="Microsoft.NET.Sdk">
  <Import Project="Directory.Build.props.user" Condition="Exists('Directory.Build.props.user')" />

  <PropertyGroup>
    <TargetFramework>netstandard2.1</TargetFramework>
    <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
    <LangVersion>latest</LangVersion>
    <RestoreAdditionalProjectSources>
      https://api.nuget.org/v3/index.json;
      https://nuget.bepinex.dev/v3/index.json
    </RestoreAdditionalProjectSources>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="BepInEx.Analyzers" Version="1.*" PrivateAssets="all" />
    <PackageReference Include="BepInEx.Core" Version="5.*" />
    <PackageReference Include="BepInEx.PluginInfoProps" Version="2.*" />
    <PackageReference Include="BepInEx.AssemblyPublicizer.MSBuild" Version="0.4.2" PrivateAssets="all" />
  </ItemGroup>

  <ItemGroup Condition="Exists('$(GameDir)')">
    <Reference Include="$(GameDir)\*_Data\Managed\Assembly-CSharp.dll" Publicize="true" Private="false" />
    <Reference Include="$(GameDir)\*_Data\Managed\UnityEngine.dll" Private="false" />
    <Reference Include="$(GameDir)\*_Data\Managed\UnityEngine.CoreModule.dll" Private="false" />
  </ItemGroup>

  <Target Name="CopyToBepInEx" AfterTargets="Build" Condition="Exists('$(GameDir)\BepInEx\plugins')">
    <Copy SourceFiles="$(TargetPath)" DestinationFolder="$(GameDir)\BepInEx\plugins\$(ProjectName)" />
    <Message Text="Copied $(TargetFileName) to $(GameDir)\BepInEx\plugins\$(ProjectName)" Importance="high" />
  </Target>
</Project>
```

## 2. Verification Commands
- **Decompile Target Class First**: `ilspycmd -t "TargetClass" "$GameDir\<Game>_Data\Managed\Assembly-CSharp.dll"`
- **Build & Auto-Deploy**: `dotnet build -c Release`
