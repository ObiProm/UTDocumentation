# StandardLoadingManager

Inherits from: [`LoadingManager`](pages/loadingmanager.md)

A standard loading manager that handles map initialization, player spawning per team, and game data synchronization between the server and clients.

## Virtual functions

Here you can see functions, which calls on some events during the loading process.

| Function | Parameters | Description |
|----------|------------|-------------|
| `ServerLoaded` | - | Calls on the server when the map and game data have been fully initialized and are ready to be sent to clients. |
| `PreClientGameDataNotify` | - | Calls on the client right before it starts processing the received game data and spawning entities. |
| `PostClientGameDataNotify` | - | Calls on the client after all map elements and players have been spawned, just before final synchronization. |

### Events

<div class="markdownTable">

| Event | Parameters | Description |
|-------|------------|-------------|
| `PlayerSpawned` | player (PlayerContrtoller) | Invoked on both the server and clients when a player character is spawned in the world. |

</div>