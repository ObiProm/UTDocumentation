## Zombie

You can spawn zombies via `game.CreateZombie(zombieId)`. Be carefull, because you must fill [zombie config](#zombies_config) before spawning it using `game.CreateZombie(zombieId)`

---

### `Zombie.InitializeModel(modelPath, isAnimated?)`

Initializes zombie model from path, if `isAnimated`, it calls "ArmatureAction" in model

#### Parameters:

- `modelPath` (`string`) — path to model
- `isAnimated` (`bool`, default: `true`) — is animated, if true calls "ArmatureAction" in model

---

### `Zombie.SpawnOnPath(path3D)`

Spawn zombie on path, it starts moving.

#### Parameters:

- `path3D` (`Path3D`) — name, which will be displayed on hover on zombie.

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
| `Health`            | `integer`, default: `5`   | Health of zombie, when `0` destroys.                                        |
| `MaxHealth`         | `integer`, default: `5`   | Max health of zombie.                                                       |
| `Speed`             | `number`, default: `2`    | Speed of zombie.                                                            |
| `Type`              | `string`                  | Name, which will be displayed on hover on zombie (if InfoShower was added). |
| `CurrentRoom`       | `Room`                    | Room which zombie belongs.                                                  |

</div>

### Fields

<div class="markdownTable">

| Event               | Parameters                | Description                                                                 |
|---------------------|---------------------------|-----------------------------------------------------------------------------|
| `OnDamageReceived`  | `Tower tower`, `int count`| Calls when zombie gets damage from `tower`, `count` - how much              |
| `OnPathEnded`       |             -             | Calls when zombie finishes their path                                       |
| `OnDeath`           |             -             | Calls when zombie dies                                                      |

</div>