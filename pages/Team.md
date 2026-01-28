# Team

Represents a team within a room, managing player membership, team color, and team health state.

## Methods

### `Team:TransferPlayerThisTeam(player)`

Transfers a player to this team. Automatically removes the player from their previous team (if any) and updates their `CurrentTeam` reference.

#### Parameters:
*   `player` (`PlayerLobby`) — The player to transfer to this team.

* * *

### `Team:RemovePlayer(player)`

Removes a player from this team and clears their `CurrentTeam` reference.

#### Parameters:
*   `player` (`PlayerLobby`) — The player to remove from the team.

* * *

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `TeamID` | `string` | Unique string identifier (GUID) of the team. Used internally for path registration, team changes, and networking. |
| `Name` | `string` | The name of the team. Default: `"Team"`. |
| `Color` | `Color` | The visual color associated with the team. Default: `Color(0, 0, 0)` (Black). |
| `PlayersCount` | `integer` | Read-only: Current number of players in the team. |
| `MaxPlayers` | `integer` | Maximum number of players allowed. `0` means unlimited. Default: `0`. |
| `MaxHealth` | `integer` | Maximum health of the team. Default: `100`. |
| `CurrentHealth` | `integer` | Current health of the team. |
| `AvalibleToAddPlayer` | `boolean` | Read-only: `true` if the team can accept more players (`PlayersCount + 1 <= MaxPlayers` or `MaxPlayers == 0`). |
| `IsAlive` | `boolean` | Read-only: `true` if `CurrentHealth > 0`. |
| `Players` | `table<number>` | Set of `PeerID`s (numbers) of the players currently in this team. |

## Example

```lua
-- Check if the team is still alive and has space
if team.IsAlive and team.AvalibleToAddPlayer then
    print("Team " .. team.Name .. " is ready for more players!")
end

-- Transfer a player to this team
local player = room.Players[targetPeerId]
if player then
    team:TransferPlayerThisTeam(player)
    print(player.PlayerName .. " joined " .. team.Name)
end

-- Iterate over all players in the team
for i, peerId in ipairs(team.Players) do
    local p = room.Players[peerId]
    if p then
        print("Team member: " .. p.PlayerName)
    end
end
```