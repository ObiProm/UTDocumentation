## Zombies Config

To define custom zombie types, create a JSON file and reference it in your mod's [main config](mainconfig.md).

All fields are optional.

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
        "ModelPath": "Scenes/NormalBoss.scn",
        "StartAnimations": ["Walk", "Idle"]
    },
    "Runner": {
        "Health": 50,
        "LuaClass": "Runner",
        "SomeCustomField": true
    }
}
```

### Fields explained

- **Health** / **MaxHealth** / **Speed** / **Type** — fields from [`Zombie`](pages/zombie.md) / [`GameEntity`](pages/GameEntity.md)
- **ModelPath** — path to `.scn` or `.glb` model. Loaded automatically by `game.CreateZombie`.
- **StartAnimations** — array of animation names; one is picked at random on spawn via `PlayAnimation`.
- **UseModelFront** — passed to `PathFollow3D.UseModelFront` for model orientation on the path.
- **LuaClass** (optional) — Lua class registered via `game.RegisterClass()` instead of default `Zombie`.

### Special behaviors

- All custom fields (e.g. `"Damage": 15`) are written to the zombie's Lua table on spawn.
- If `Type` is omitted, the JSON key is used as the display name.
- If only `Health` or `MaxHealth` is set, the other matches it automatically.

Place config files in any subfolder of `Configs/Zombies/`.
