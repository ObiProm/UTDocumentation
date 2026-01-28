# Scene Architecture

When you press "Start game" in the lobby, the game creates a complex hierarchy of nodes for each room. Understanding this architecture is crucial for modding.

## RoomGameScene

For each room, the game creates a `RoomGameScene` node in the root. This node serves as the container for all gameplay systems.

```text
Root
├── game_room_0        ← RoomGameScene for room "room_0"
|  └── LoadingManager
├── game_room_1        ← RoomGameScene for room "room_1"
|  └── LoadingManager
```

You can access it via `game.GetRoomGameScene(room)` or `self:GetParent()` if your code is inside the scene.

## LoadingManager

After creating `RoomGameScene`, the game reads the gamemode config and instantiates the `LoadingManager`. 

The **base LoadingManager** is responsible for initializing the core Tower Defense systems. It automatically creates the following nodes as children of `RoomGameScene`:

| Manager | Purpose | Execution Context |
|---------|---------|-------------------|
| `EconomyManager` | Handles currencies and purchases | Server & All Clients |
| `TowerPlacementManager` | Handles tower placement logic | Server & All Clients |
| `TowerManager` | Manages all towers in the game | Server & All Clients |
| `PathManager` | Manages zombie paths | Server & All Clients |
| `RaycastManager` | Handles raycasting for interactions | **Local player only** |
| `InfoShower` | Shows tower/zombie info on hover | **Local player only** |
| `UpgradeMenu` | Tower upgrade interface | **Local player only** |

### StandardLoadingManager

The game provides a built-in `StandardLoadingManager` which is used by default maps. It inherits from the base `LoadingManager` and adds two critical features:
1. **Map Loading:** It reads the map configuration and spawns the actual map layout (walls, paths, decorations).
2. **PlayerController:** It spawns the `PlayerController` node, which handles the local player's camera, movement, and input.

### Submodules Initialization

During the loading process, the game also attaches Submodules directly to the `RoomGameScene` as child nodes. This is why Submodules (which we will cover in the next article) are active across all gamemodes — they simply live inside the room's scene hierarchy.

## Accessing Managers

To access these managers in your code, you can get them directly from the `RoomGameScene`:

```lua
-- Get the RoomGameScene
local roomGameScene = game.GetRoomGameScene(room)

-- Access managers directly (they are public fields)
local economyManager = roomGameScene.EconomyManager
local towerManager = roomGameScene.TowerManager
local pathManager = roomGameScene.PathManager
```