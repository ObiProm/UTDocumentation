# PathManager

A node responsible for managing navigation or movement paths associated with specific teams. It maps each `Team` to a `Path3D` node.

## Methods

### `PathManager:RegisterPath(team, path)`

Registers a path for a specific team. If a path is already registered for this team, it will not be overwritten.

#### Parameters:
*   `team` (`Team`) — The team to associate the path with.
*   `path` (`Path3D`) — The `Path3D` node representing the path.

* * *

### `PathManager:GetZombiesCountOnTeamPath(team): number`

Returns the number of zombies currently on the path assigned to the specified team. Counts only `Zombie` nodes on the path — not all child nodes.

#### Parameters:
*   `team` (`Team`) — The team whose path count you want to retrieve.

#### Returns:
*   `number` — The number of zombies on the path, or `-1` if no path is registered for the team.

* * *

### `PathManager:GetPaths(): table`

Retrieves the entire mapping of teams to their registered paths.

#### Returns:
*   `table` — A dictionary where keys are `TeamID` (`string`) and values are `Path3D` nodes.

#### Example:
```lua
local allPaths = pathManager:GetPaths()
for teamId, path in pairs(allPaths) do
    local team = room.Teams[teamId]
    local count = pathManager:GetZombiesCountOnTeamPath(team)
    print("Team " .. team.Name .. " has " .. count .. " zombies on path")
end
```