# Recipe: Minecraft Java Modding (Fabric or NeoForge)

## When to Use
Use this recipe when creating a Minecraft Java Edition mod (1.20.x / 1.21+).
- Choose **Fabric** for fast version updates, lightweight client/server mods, and clean Mixin hooks.
- Choose **NeoForge** for large multi-system content/tech mods with built-in capability/event buses.

## 1. Environment Check (Java 21 Required for MC 1.20.5+ / 1.21+)
```powershell
java -version
# If Java 21 is missing, ask user to run: winget install EclipseAdoptium.Temurin.21.JDK
```

## 2. Recommended Directory Layout (Gradle)
```text
├── gradle.properties     # minecraft_version, loader_version, mod_id
├── build.gradle
└── src/main/
    ├── java/com/example/modid/
    │   ├── ModInitializer.java
    │   ├── mixin/        # @Mixin classes (@Inject, @ModifyReturnValue via MixinExtras)
    │   ├── item/         # Custom items
    │   └── block/        # Custom blocks & entities
    └── resources/
        ├── fabric.mod.json (or META-INF/neoforge.mods.toml)
        ├── modid.mixins.json
        └── assets/modid/ # textures, models, lang/en_us.json
```

## 3. Mixin Best Practice
Prefer **MixinExtras** (`@ModifyReturnValue`, `@WrapOperation`, `@ModifyExpressionValue`) over destructive `@Redirect` or cancelling `@Inject` callbacks so your mod stays compatible with other mods!

## 4. Verification Commands
- **Compile & Verify Mixins**: `.\gradlew build`
- **Launch Dev Client**: `.\gradlew runClient`
