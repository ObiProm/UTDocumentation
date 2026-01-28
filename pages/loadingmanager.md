## LoadingManager

Base class for game loading managers. Responsible for preparing the game environment before starting. You need to inherit from this class and register your custom manager in the gamemode config.

### Functions

### `LoadingManager.Initialize(room)`

Initializes the loading manager with room data. This method is called automatically when the game starts.

**Parameters:**
- `room` (`Room`) — Room object containing game settings, teams, and players information

---

### `LoadingManager.SendReady()`

Notifies the system that this client has finished loading and is ready to start the game. Should be called after all resources are loaded.

---

### Events

<div class="markdownTable">

| Field                        | Parameters          | Description |
|------------------------------|---------------------|-------------|
| `OnAllPlayersLoaded`         | -                   | Emitted when all players in the room have finished loading and sent their ready status. |

</div>

## Usage Guide

### Creating a Custom Loading Manager

1. **Create a new Lua class** that inherits from `LoadingManager`:
```lua
---@class MyCustomLoadingManager : LoadingManager
local MyCustomLoadingManager = {}

function MyCustomLoadingManager:Initialize(room)
    -- Create RPC node for network communication
    self.RpcNode = game.CreateNode("RpcNode")
    self.RpcNode.Name = "RpcNode"
    self.RpcNode:BindLuaTable(self)
    self:AddChild(self.RpcNode)
    
    -- Connect to the all players loaded signal
    self.OnAllPlayersLoaded.Connect(function()
        -- Start your game logic here
        print("All players loaded! Starting game...")
    end)
    
    -- Handle server/client logic
    if IsServer() then
        -- Server-side initialization
        self:InitializeServer(room)
    else
        -- Client-side initialization
        self.RpcNode:RpcIdReliable(1, "ServerBaseLoaded")
    end
end

function MyCustomLoadingManager:InitializeServer(room)
    -- Server-specific setup
    -- Load maps, spawn players, etc.
    
    -- Notify clients when ready
    self.ServerLoaded = true
end

function MyCustomLoadingManager:ServerBaseLoaded()
    local senderId = self.RpcNode.SenderId
    if IsServer() and self.ServerLoaded then
        -- Send game data to client
        self.RpcNode:RpcIdReliable(senderId, "ClientGameDataNotify", self.gameData)
    end
end

function MyCustomLoadingManager:ClientGameDataNotify(data)
    -- Client receives game data from server
    -- Load resources, spawn UI, etc.
    
    -- Call when finished loading
    self:SendReady()
end

-- Register the class
game.RegisterClass("MyCustomLoadingManager", MyCustomLoadingManager, "LoadingManager")
```

### Registering in Gamemode Config

In your gamemode configuration file you must place name of class into `LoadingManagerScript`.

```json
{
    "Name": "MyCustomGamemode",
    "LoadingManagerScript": "MyCustomLoadingManager",
    "Map": "res://Maps/MyMap.tscn"
}
```

<p> See also <a href="#gamemodesconfig">gamemode configuration file</a> </p>

### Key Concepts

- **RoomGameScene**: The root node created for each game room, named `game_<room_id>`. Your loading manager is added as a child to this node.
- **RPC Communication**: Use `RpcNode` for reliable network communication between server and clients during loading.
- **Loading UI**: Use `LoadingUI` class to show progress to players:
  ```lua
  LoadingUI.SetStatus("Loading maps...")
  LoadingUI.SetPercentage(25)
  ```
- **Network Roles**: Check `IsServer()` to determine if current instance is server or client.
- **Resource Loading**: Use `game.GetMap()`, `game.GetPlayerPacked()`, and `game.GetUIPacked()` to load game resources.