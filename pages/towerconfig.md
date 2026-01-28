# TowerConfig

Represents configuration data for a tower type, including its base stats, upgrade paths, and visual properties.

## Fields

| Field | Type | Description |
|-------|------|-------------|
| PrintName | string | Display name of the tower shown in UI (e.g., "Machine Gun Tower"). |
| Icon | string | Resource path to the tower's icon image (e.g., "res://Assets/Icons/Towers/machine_gun.png"). |
| PlacementCost | number | Resource cost required to place this tower initially. |
| LockPathLevel | number | Level at which upgrade paths become locked (prevents further upgrades on that path). |
| UpgradePathsCount | number | Read-only: Number of available upgrade paths for this tower (automatically calculated from UpgradePaths array). |
| Scene | string | Resource path to the tower's scene file (e.g., "res://Scenes/Towers/MachineGun.tscn"). |
| BaseStats | table | Dictionary containing the tower's base statistics (e.g., {damage = 10, range = 100, fire_rate = 2.0}). |
| UpgradePaths | array<table> | Array of upgrade path configurations, where each path contains level-specific stat modifications (e.g., {{level_1 = {damage = 5}}, {level_1 = {range = 20}}}). |

## Example usage:

```lua
-- Get tower configuration
local config = game.GetTowerConfig("MachineGunTower")

-- Access base properties
print("Tower Name: " .. config.PrintName)
print("Placement Cost: " .. config.PlacementCost)

-- Access base stats
print("Base Damage: " .. config.BaseStats.damage)
print("Base Range: " .. config.BaseStats.range)

-- Iterate through upgrade paths
for pathIndex, path in ipairs(config.UpgradePaths) do
    print("Upgrade Path " .. pathIndex)
    for level, stats in pairs(path) do
        print("  Level " .. level .. ": +" .. stats.damage .. " damage")
    end
end

-- Create actual tower instance
local tower = game.CreateTower("MachineGunTower")
tower.Position = Vector3(10, 0, 20)
```

Note: This configuration is typically loaded from JSON or resource files and represents the blueprint for tower instances. The BaseStats and UpgradePaths dictionaries follow flexible schemas defined by your game's tower system.
```