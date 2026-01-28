## Zombie

Inherits from: [`GameEntity`](pages/GameEntity.md) → `Node3D`

You can spawn zombies via `game.CreateZombie(zombieId)`. Be carefull, because you must fill [zombie config](pages/zombies_config.md) before spawning it.

---

### `Zombie.InitializeModel(modelPath, isAnimated?)`

Initializes zombie model from path, if `isAnimated`, it calls "ArmatureAction" in model

#### Parameters:

- `modelPath` (`string`) — path to model
- `isAnimated` (`bool`, default: `true`) — is animated, if true calls "ArmatureAction" in model

---

### `Zombie.PlayAnimation(name)`

Plays an animation on the loaded model.

#### Parameters:

- `name` (`string`) — animation name

---

### `Zombie.SpawnOnPath(path3D)`

Spawns zombie on path and starts movement along it.

#### Parameters:

- `path3D` (`Path3D`) — path to follow

> `CurrentRoom` and `CurrentTeam` must be set before spawning.

---

### `Zombie.GetDamage(tower, damage)`

Zombie will receive damage in count `damage`.

#### Parameters:

- `tower` (`Tower`) — tower, which dealt damage.
- `damage` (`integer`) — how much damage.

---

### Fields

<div class="markdownTable">

| Field               | Type                      | Description                                                                 |
|---------------------|---------------------------|-----------------------------------------------------------------------------|
| `Speed`             | `number`, default: `2`    | Speed of zombie.                                                            |
| `Type`              | `string`                  | Name, which will be displayed on hover on zombie (if InfoShower was added). |

</div>

> Shared fields and events (`Health`, `CurrentRoom`, `OnDeath`, etc.) — see [`GameEntity`](pages/GameEntity.md).

### Events

<div class="markdownTable">

| Event               | Parameters                | Description                                                                 |
|---------------------|---------------------------|-----------------------------------------------------------------------------|
| `OnPathEnded`       |             -             | Calls when zombie finishes their path                                       |

</div>

## Virtual functions

Here you can see functions, which calls on some events, like `OnTowerPlaced` in example in the start of this page.

| Function | Parameters | Description |
|----------|------------|-------------|
| `ProcessTargetSelect` | `tower (Tower)` | return `False` to prevent tower target selecting |
| `ProcessTargetExit` | `tower (Tower)` | return `False` to prevent tower target exiting |