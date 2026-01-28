# GameEntity

Inherits from: `Node3D`

Base class for all combat entities in the game. [`Tower`](pages/tower.md) and [`Zombie`](pages/zombie.md) inherit from it.

```
Node3D → GameEntity → Tower / Zombie
```

Provides shared health, room/team context, and hooks into the [Effects system](pages/EffectsSystem.md).

---

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `Health` | `integer` | Current health. When it reaches `0`, the entity is destroyed. Default: `50`. |
| `MaxHealth` | `integer` | Maximum health. If set to `0`, the HP bar is hidden in the info panel. Default: `100`. |
| `CurrentRoom` | `Room` | Room this entity belongs to. |
| `CurrentTeam` | `Team` | Team this entity belongs to. |

---

## Events

| Event | Parameters | Description |
|-------|------------|-------------|
| `OnDamageReceived` | `Tower tower`, `int health` | [`LuaEvent`](pages/luaevent.md). Fires when the entity receives damage. `health` is remaining HP after the hit. |
| `OnDeath` | — | Fires when the entity dies. |

---

## Methods

### `GameEntity.GetBaseStat(statName): number`

Returns the base value of a stat **before** active effects are applied.

#### Parameters:

- `statName` (`string`) — stat name (e.g. `"Damage"`, `"Speed"`)

#### Returns:

- `number` — unmodified base value

---

### `GameEntity.ModifyBaseStat(statName, delta): void`

Permanently changes a base stat by `delta` and writes the result to the entity's Lua fields.

#### Parameters:

- `statName` (`string`) — stat name
- `delta` (`number`) — amount to add

---

### `GameEntity.GiveEffect(effectData): string`

Applies a buff/debuff and recalculates stats. See [Effects system](pages/EffectsSystem.md) for the `effectData` format.

#### Returns:

- `string` — GUID of the applied effect, or `nil` if blocked by `ProcessEffect`

---

### `GameEntity.RemoveEffect(guid): void`

Removes an effect by GUID and recalculates stats.

#### Parameters:

- `guid` (`string`) — GUID returned by `GiveEffect`

---

## Virtual functions

| Function | Parameters | Description |
|----------|------------|-------------|
| `ProcessEffect` | `effectData` | Called before an effect is applied. Return `false` to reject it. |
| `OnStatsRecalculated` | — | Called after stats are recalculated. |

---

## Example

```lua
function MyZombie:ProcessEffect(effectData)
    if effectData.Source == "EnemySlow" then
        return false
    end
end

function MyTower:OnStatsRecalculated()
    print("Damage is now", self.Damage)
end
```
