# PlayerLobby

Represents a player in the lobby or a room.

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `PeerID` | `number` | Network ID of the player (64-bit integer, represented as number in Lua). |
| `PlayerName` | `string` | Display name of the player. |
| `Inventory` | `table<string>` | List of items in player's inventory (e.g. `{"Agent"}`). |
| `Disconnected` | `fun() \| nil` | Callback invoked when player disconnects. |
| `CurrentRoom` | `Room \| nil` | Reference to the room the player is currently in. |
| `CurrentTeam` | `Team \| nil` | Reference to the team the player is currently assigned to. |
| `IsRoomAdmin` | `boolean` | Read-only: `true` if this player is the admin of the current room. |