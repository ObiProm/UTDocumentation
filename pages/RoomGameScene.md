# RoomGameScene

Represents an RoomGameScene, its created to divide match for each room

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `EconomyManager` | `EconomyManager` | Gets economy manager for this room . |
| `TowerPlacementManager` | `TowerPlacementManager` | Gets tower placement manager for this room . |
| `TowerManager` | `TowerManager` | Gets tower manager for this room.  |
| `PathManager` | `PathManager` | Gets path manager for this room. |

## Example

```lua
local roomGameScene = game.GetRoomGameScene(room)
    self.EconomyManager = roomGameScene.EconomyManager
    self.TowerManager = roomGameScene.TowerManager
    self.PathManager = roomGameScene.PathManager

    -- Register/add currency for room
    self.EconomyManager:RegisterCurrency("Money", "$", 300)
    self.EconomyManager:AddCurrency(playerID, "Money", 100)

    -- Do something with towers
    self.TowerManager:CallForAllTowers("OnWaveStarted", self.Wave)

    -- Or spawn zombie
    for teamId, path in pairs(self.PathManager:GetPaths()) do
        local zombie = game.CreateZombie(type)
        zombie.CurrentRoom = self.CurrentRoom
        zombie.Name = zombieID

        zombie:SpawnOnPath(path)
    end
```