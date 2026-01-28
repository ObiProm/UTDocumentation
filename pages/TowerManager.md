# TowerManager

A node responsible for managing all active towers in the game. It tracks towers by their unique GUIDs, owners, and teams, and handles their lifecycle (placement and removal).

## Methods

### `TowerManager:AddTower(tower, guid, ownerId)`

Manually registers a tower instance with the manager. This is typically called automatically when a tower is placed via the `TowerPlacementManager`.

#### Parameters:
*   `tower` (`Tower`) — The tower instance to register.
*   `guid` (`string`) — The unique identifier for the tower.
*   `ownerId` (`number`) — The PeerID of the player who owns this tower.

* * *

### `TowerManager:FreeTower(guid)`

Removes and frees a tower by its unique GUID. This will also remove it from the owner's list and trigger cleanup logic.

#### Parameters:
*   `guid` (`string`) — The unique identifier of the tower to remove.

* * *

### `TowerManager:FreeTower(tower)`

Removes and frees a tower by passing its Lua table reference.

#### Parameters:
*   `tower` (`table`) — The Lua table representing the tower to remove.

* * *

### `TowerManager:GetTowerByGuid(guid): table`

Retrieves the Lua table representation of a tower by its unique GUID.

#### Parameters:
*   `guid` (`string`) — The unique identifier of the tower.

#### Returns:
*   `table` — The Lua table for the tower, or `nil` if not found.

* * *

### `TowerManager:GetTowersByOwner(ownerId): table`

Retrieves a list of all towers owned by a specific player.

#### Parameters:
*   `ownerId` (`number`) — The PeerID of the owner.

#### Returns:
*   `table` — An array-like table of Lua tables representing the towers.

* * *

### `TowerManager:GetTowersByOwner(player): table`

Retrieves a list of all towers owned by a specific player.

#### Parameters:
*   `player` (`PlayerLobby`) — The player instance.

#### Returns:
*   `table` — An array-like table of Lua tables representing the towers.

* * *

### `TowerManager:GetTowersByTeam(team): table`

Retrieves a list of all towers belonging to a specific team.

#### Parameters:
*   `team` (`Team`) — The team instance.

#### Returns:
*   `table` — An array-like table of Lua tables representing the towers.

* * *

### `TowerManager:GetAllTowers(): table`

Retrieves a list of all currently active towers in the game.

#### Returns:
*   `table` — An array-like table of Lua tables representing all towers.

* * *

### `TowerManager:CallForAllTowers(method, ...)`

Calls a specific function on the Lua table of every active tower. Useful for global updates or synchronization.

#### Parameters:
*   `method` (`string`) — The name of the function to call on each tower's Lua table.
*   `...` — Arguments to pass to the function.

#### Example:
```lua
-- Call a hypothetical 'UpdateStatus' function on every tower
towerManager:CallForAllTowers("UpdateStatus", "active")
```

* * *

### `TowerManager:ClearAllTowers()`

Immediately removes all towers from the manager's internal tracking lists without freeing the nodes themselves. Use with caution.