# Effects System

Buff/debuff system for [`GameEntity`](pages/GameEntity.md) objects (`Tower`, `Zombie`). Automatically recalculates stats when effects are applied or removed.

Supports stacking multipliers, non-stacking "best effect" selection, and respects the `LowerBetter` config marker (e.g., reducing a zombie's `Speed` or a tower's `Cooldown` is treated as a positive buff).

Use `GiveEffect` and `RemoveEffect` from [`GameEntity`](pages/GameEntity.md). To block effects, override `ProcessEffect` in your Lua class.

---

## Effect data structure

The `effectData` argument supports the following keys:

| Key | Type | Required | Default | Description |
|-----|------|----------|---------|-------------|
| `Stat` | `string` | **Yes** | - | The name of the stat to modify (e.g., `"Damage"`, `"Speed"`). |
| `Value` | `number` | **Yes** | - | The multiplier to apply. `1.5` means +50%, `0.8` means -20%. |
| `StackMode` | `string` | No | - | `"Stack"`: multiplies with all other stacking effects on this stat.<br>`"None"` (or any other string): only the effect with the **highest** `Value` applies. Others stay in memory until they expire. |
| `StackType` | `string` | No | - | `"Multiplicative"` or `"Additive"`. Only used when `StackMode = "Stack"`. |
| `Duration` | `number` | No | permanent | Duration in seconds. `<= 0` or omitted means permanent until manually removed. |
| `MinValue` | `number` | No | `-∞` | Floor for the final calculated stat (e.g., `Cooldown` cannot go below `0.1`). |
| `Source` | `string` | No | `nil` | Optional identifier for grouping/debugging. |

---

## Example

```lua
-- Temporary 50% damage buff for 10 seconds
local buffGuid = self:GiveEffect({
    Stat = "Damage",
    Value = 1.5,
    StackMode = "Stack",
    Duration = 10.0
})

-- Permanent speed reduction; if a stronger slow exists, this one is ignored
local slowGuid = self:GiveEffect({
    Stat = "Speed",
    Value = 0.8,
    StackMode = "None",
    Source = "MyMod_SlowAura"
})

self:RemoveEffect(buffGuid)
```
