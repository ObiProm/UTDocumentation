# Room

Represents an active room instance.

## Methods

### `Room:JoinPlayer(player)`

Adds a player to the room, automatically assigns them to the smallest available team, and updates their `CurrentRoom` reference. If the room reaches `MaxPlayers`, it becomes hidden from the public list.

#### Parameters:
*   `player` (`PlayerLobby`) — The player to join.

* * *

### `Room:AddPlayer(player)`

Adds a player to the room's player list without automatically assigning them to a team. 

#### Parameters:
*   `player` (`PlayerLobby`) — The player to add.

* * *

### `Room:RemovePlayer(playerId)`

Removes a player from the room, clears their team assignment, and updates their `CurrentRoom` to `nil`. If the removed player was the Admin, the admin role is passed to the next available player. If the room is no longer full and the game hasn't started, it becomes visible again.

#### Parameters:
*   `playerId` (`number`) — The network ID (PeerID) of the player to remove.

* * *

### `Room:AddTeam(team)`

Adds a new team to the room. Any players currently assigned to a team with the same name will be updated to reference this new team instance.

#### Parameters:
*   `team` (`Team`) — The team instance to add.

* * *

### `Room:RemoveTeam(teamName): boolean`

Removes a team from the room. Automatically redistributes the team's players to other available teams based on free space. 

#### Parameters:
*   `teamName` (`string`) — The name of the team to remove.

#### Returns:
*   `boolean` — `true` if the team was successfully removed and players redistributed, `false` if there is not enough space in other teams.

* * *

### `Room:RenameTeam(oldName, newName)`

Changes the name of an existing team and updates the room's team dictionary.

#### Parameters:
*   `oldName` (`string`) — The current name of the team.
*   `newName` (`string`) — The new name for the team.

* * *

### `Room:ChangePlayerTeam(playerId, teamName)`

Moves a specific player to a different team within the room.

#### Parameters:
*   `playerId` (`number`) — The network ID (PeerID) of the player.
*   `teamName` (`string`) — The name of the target team.

* * *

### `Room:GetTeamPlayers(teamName): table`

Retrieves an array-like table of all players currently in the specified team.

#### Parameters:
*   `teamName` (`string`) — The name of the team.

#### Returns:
*   `table` — An array of `PlayerLobby` instances.

* * *

### `Room:AddPlayerToSmallestTeam(player)`

Finds the team with the fewest players that can accept new members and assigns the player to it. If no teams are available, creates a new fallback team (e.g., "Team0").

#### Parameters:
*   `player` (`PlayerLobby`) — The player to assign.

* * *

### `Room:GetPlayerList(): table`

Retrieves a list of all players currently in the room.

#### Returns:
*   `table` — An array-like table of `PlayerLobby` instances.

* * *

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `RoomId` | `string` | Unique identifier for the room. |
| `RoomName` | `string` | Display name of the room. |
| `MaxPlayers` | `integer` | Maximum number of players allowed. |
| `Settings` | `RoomSettings` | Game settings (map, mode, etc.). |
| `PlayersCount` | `integer` | Read-only: current number of connected players. |
| `Players` | `table<number, PlayerLobby>` | Map of `PeerID` → `PlayerLobby` instances. |
| `Teams` | `table<string, Team>` | Map of team name → `Team` instances. |
| `Password` | `string` | Room password; empty string means no password. |
| `IsVisible` | `boolean` | Whether the room appears in the public room list. Automatically updates based on player count and game state. |
| `GameStarted` | `boolean` | `true` if the game has started and players can no longer join. |
| `Admin` | `PlayerLobby` | The player who owns/created the room. Automatically updates if the admin leaves. |

### Events

<div class="markdownTable">

| Event | Parameters | Description |
|-------|------------|-------------|
| `BecomeEmpty` | - | Invoked when the last player leaves the room, making the player count zero. |

</div>

## Example

```lua
-- Iterate all players using the dedicated method
local allPlayers = room:GetPlayerList()
for i, player in ipairs(allPlayers) do
    print("Player in room: " .. player.PlayerName)
end

-- Move a player to a specific team
room:ChangePlayerTeam(targetPeerId, "Red")

-- Safely remove a team (returns false if players can't be redistributed)
local success = room:RemoveTeam("Spectator")
if not success then
    print("Cannot remove team: not enough space in other teams")
end

-- Check admin
if room.Admin.PeerID == myPeerId then
    print("I am the room owner")
end
```