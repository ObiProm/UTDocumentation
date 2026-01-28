# Networking

Uninfected Tower is a multiplayer game. Your mod code runs on **both** the client and the server. If you change a variable on the client, it won't automatically change on the server, and vice versa.

To synchronize actions between the client and server, you need to use **Remote Procedure Calls (RPC)** via `RpcNode`.

## Creating an RpcNode

`RpcNode` is a specialized node for network communication. Regular nodes don't support RPC — you must create an `RpcNode` explicitly.

### Standard Setup Pattern

```lua
local MyNetworkedClass = {}

function MyNetworkedClass:_Init()
    self.RpcNode = game.CreateNode("RpcNode")
    self.RpcNode.Name = "RpcNode"
    self.RpcNode:BindLuaTable(self)  -- Bind 'self' so RPC can call methods on this instance
    self:AddChild(self.RpcNode)
end

-- This method can be called remotely via RPC
function MyNetworkedClass:OnDamageReceived(amount)
    print("Received " .. amount .. " damage!")
end

game.RegisterClass("MyNetworkedClass", MyNetworkedClass)
```

> ⚠️ **Important:** All RPC methods **must use `:` (colon)**, not `.` (dot). The first argument is always `self`.

### Supported Data Types
RPC supports only: `number`, `string`, `boolean`, `Vector2`, `Vector3`, `Color`, `table`. You cannot send custom userdata or functions.

## Sending RPCs

Every client has a unique **ID**. The server always has **ID = 1**.

### Sending Methods

| Method | Target | Use Case |
|--------|--------|----------|
| `RpcIdReliable(id, method, ...)` | Specific client (use `1` for server) | Critical actions: purchases, damage, state changes |
| `RpcIdUnreliable(id, method, ...)` | Specific client | Frequent updates: position sync, animations |
| `RpcReliable(method, ...)` | All clients | Broadcast critical updates to everyone |
| `RpcUnreliable(method, ...)` | All clients | Broadcast frequent updates |
| `RpcRoomReliable(room, method, ...)` | All clients in a room | Room-specific critical updates |
| `RpcRoomUnreliable(room, method, ...)` | All clients in a room | Room-specific frequent updates |

### Reliable vs Unreliable

- **Reliable**: Guaranteed delivery, slower. Use for critical game state (purchases, damage, spawning).
- **Unreliable**: May be dropped, faster. Use for frequent updates where old data is useless (position sync).

### Example: Client Requests Tower Purchase

```lua
-- Client side
function TowerPlacer:OnBuyButtonClicked(towerName, position)
    -- Send request to server (ID = 1)
    self.RpcNode:RpcIdReliable(1, "RequestBuyTower", towerName, position)
end
```

## Getting the Sender ID

When the server receives an RPC, you often need to know **which client** sent it. Use `self.RpcNode.SenderId` inside the RPC handler.

```lua
-- Server side
function TowerManager:RequestBuyTower(towerName, position)
    local senderId = self.RpcNode.SenderId
    print("Client " .. senderId .. " wants to buy " .. towerName)
    
    -- Now you can validate and respond to this specific client
    if self:CanAfford(senderId, towerName) then
        self:DeductMoney(senderId, towerName)
        self:SpawnTower(towerName, position)
        
        -- Notify the sender
        self.RpcNode:RpcIdReliable(senderId, "OnPurchaseResult", true, "Success!")
    else
        self.RpcNode:RpcIdReliable(senderId, "OnPurchaseResult", false, "Not enough money!")
    end
end
```

> 💡 `SenderId` is automatically set by the RPC system when a method is called remotely. You don't need to pass it manually.

## Complete Example: Tower Purchase Flow

### Client Side

```lua
local TowerPlacer = {}

function TowerPlacer:_Init()
    self.RpcNode = game.CreateNode("RpcNode")
    self.RpcNode.Name = "RpcNode"
    self.RpcNode:BindLuaTable(self)
    self:AddChild(self.RpcNode)
end

function TowerPlacer:OnBuyButtonClicked(towerName, position)
    self.RpcNode:RpcIdReliable(1, "RequestBuyTower", towerName, position)
end

function TowerPlacer:OnPurchaseResult(success, message)
    if success then
        print("Purchase successful: " .. message)
    else
        print("Purchase failed: " .. message)
    end
end

game.RegisterClass("TowerPlacer", TowerPlacer)
```

### Server Side

```lua
local TowerManager = {}

function TowerManager:_Init()
    self.RpcNode = game.CreateNode("RpcNode")
    self.RpcNode.Name = "RpcNode"
    self.RpcNode:BindLuaTable(self)
    self:AddChild(self.RpcNode)
end

function TowerManager:RequestBuyTower(towerName, position)
    local senderId = self.RpcNode.SenderId
    local cost = 100
    
    if self:GetPlayerMoney(senderId) >= cost then
        self:DeductMoney(senderId, cost)
        self:SpawnTower(towerName, position)
        self.RpcNode:RpcIdReliable(senderId, "OnPurchaseResult", true, "Tower purchased!")
    else
        self.RpcNode:RpcIdReliable(senderId, "OnPurchaseResult", false, "Not enough money!")
    end
end

function TowerManager:GetPlayerMoney(clientId)
    return 1000  -- Simplified
end

function TowerManager:DeductMoney(clientId, amount)
    -- Deduct logic
end

function TowerManager:SpawnTower(towerName, position)
    print("Spawning " .. towerName .. " at " .. tostring(position))
end

game.RegisterClass("TowerManager", TowerManager)
```