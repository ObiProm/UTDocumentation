## RpcNode

A specialized node for remote procedure calls (RPC). Regular nodes do not support RPC by default. It supports only next types: `number`, `string`, `boolean`, `Vector2`, `Vector3`, `Color`, `table`.

All clients have an **ID** for sending an rpc to that specific client. If you want to send an rpc request to a server, it has an **ID of 1**.

**Warning** to avoid code execution errors, you need to create functions using ":"(colon) not "."(dot) since the first argument will be self

* * *

### `RpcNode:BindLuaTable(table)`

Binds a Lua table to the node to handle incoming RPC calls.

#### Parameters:

*   `table` (`table`) — Table containing callable methods.

#### Example:

```lua
local handlers = { 
    OnPlayerJoin = function(self, name) print(name .. " joined") end 
} 
rpcNode:BindLuaTable(handlers) 
```

* * *

### `RpcNode:GetLuaTable(): table`

Retrieves the bound Lua table.

#### Returns:

*   `table` — The bound table, or nil if none.

* * *

### `RpcNode:RpcReliable(methodName, ...)`

Sends a reliable RPC call to all connected clients.

#### Parameters:

*   `methodName` (`string`) — Name of the method to call.
*   `...` — Arguments (supports: `number`, `string`, `boolean`, `Vector2`, `Vector3`, `Color`, `table`).

#### Example:

```lua
rpcNode:RpcReliable("SyncPosition", Vector3(100, 5, 200))
```

* * *

### `RpcNode:RpcUnreliable(methodName, ...)`

Sends an unreliable RPC call to all connected clients (faster, but may be dropped).

#### Parameters:

*   `methodName` (`string`) — Name of the method to call.
*   `...` — Arguments (supports: `number`, `string`, `boolean`, `Vector2`, `Vector3`, `Color`, `table`).

* * *

### `RpcNode:RpcIdReliable(reciever, methodName, ...)`

Sends a reliable RPC call to a specific client by ID (Send to server if ID = 1).

#### Parameters:

*   `reciever` (`number`) — Client ID.
*   `methodName` (`string`) — Name of the method to call.
*   `...` — Arguments (supports: `number`, `string`, `boolean`, `Vector2`, `Vector3`, `Color`, `table`).

* * *

### `RpcNode:RpcIdUnreliable(reciever, methodName, ...)`

Sends a unreliable RPC call to a specific client by ID (Send to server if ID = 1).

#### Parameters:

*   `reciever` (`number`) — Client ID.
*   `methodName` (`string`) — Name of the method to call.
*   `...` — Arguments (supports: `number`, `string`, `boolean`, `Vector2`, `Vector3`, `Color`, `table`).

---

### `RpcNode:RpcRoomReliable(room, methodName, ...)` 

Sends a reliable RPC call to a specific room

#### Parameters: 
- `room` (`Room`) — Room, to call - `methodName` (`string`) — Name of the method to call. 
- `...` — Arguments 

--- 

### `RpcNode:RpcRoomUnreliable(room, methodName, ...)` 
Sends a unreliable RPC call to a specific rool #### Parameters: 
- `room` (`Room`) — Room, to call 
- `methodName` (`string`) — Name of the method to call.
- `...` — Arguments