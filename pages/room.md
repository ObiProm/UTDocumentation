# Room

Represents an active room instance.

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `Info` | `RoomInfo` | Basic metadata about the room. |
| `PlayersCount` | `integer` | Read-only: current number of connected players. |
| `Players` | `table<number, PlayerLobby>` | Map of `PeerID` → `PlayerLobby` instances. |
| `Teams` | `table<string, Team>` | Map of name → `Team` instances. |
| `Password` | `string` | Room password; empty string means no password. |
| `IsVisible` | `boolean` | Whether the room appears in the public room list. |
| `GameStarted` | `boolean` | `true` if the game has started and players can no longer join. |
| `Admin` | `PlayerLobby` | The player who owns/created the room. |
| `BecomeEmpty` | `fun() \| nil` | Event callback triggered when the last player leaves the room. |

## Example
```lua
-- Iterate all players
for peerId, player in pairs(room.Players) do
    print(player.PlayerName)
end

-- Check admin
if room.Admin.PeerID == myPeerId then
    print("I am the room owner")
end
```