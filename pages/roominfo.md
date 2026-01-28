# RoomInfo

Metadata about a room, used for room listing.

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `RoomId` | `string` | Unique identifier for the room. |
| `RoomName` | `string` | Display name of the room. |
| `MaxPlayers` | `integer` | Maximum number of players allowed. |
| `Settings` | `RoomSettings` | Game settings (map, mode, etc.). |
| `PlayersCount` | `integer` | Current number of players in the room. |