## Zombies Config

To define custom zombie types, create a JSON file and reference it in your mod's [main config](mainconfig.md).

In this config **all fields are optional**!

```json
{
    "Normal": {
        "Health": 4,
        "Speed": 4,
        "ModelPath": "Scenes/NormalZombie.scn"
    },
    "NormalBoss": {
        "Type": "Normal boss",
        "Health": 100,
        "Speed": 3,
        "ModelPath": "Scenes/NormalBoss.scn"
    },
    "Runner": {
        "Health": 50,
        "LuaClass": "Runner",
        "SomeCustomField": true,
    }
}
```

### Fields explained

- **Health** / **MaxHealth** / **Speed** / **Type** - fields from base `Zombie` class
- **ModelPath** - Path to `.scn` scene file for the zombie model. When set:
  - Spawns the specified 3D model
  - Automatically activates `ArmatureAction` animation state
- **LuaClass** (optional) - Name of a Lua class to instantiate instead of default behavior:
  - Must be a valid class registered via `game.RegisterClass()`


### Special behaviors

- All fields, also custom (e.g., `"Damage": 15`, `"ExplosionRadius": 3`) are passed directly to the zombie's Lua table during spawn events. Because of that you can set fields into `Zombie` class and add anything yours

- If `Type` omitted, the zombie's ID (JSON key) is used instead
  
- If from `Health` and `MaxHealth` only one is specified, the other automatically matches it. Example: `"Health": 50` implies `"MaxHealth": 50`

Add your zombies config to the [main config](mainconfig.md):
```json
{
    "ZombiesConfig": "Zombies.json"
}
```
