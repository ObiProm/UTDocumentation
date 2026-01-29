# Node

Base class for all scene objects. All other objects you use are derived from it.

## Virtual Functions

| Function | Description |
|----------|-------------|
| `_Init` | Called when node is created by `game.CreateNode()`. |
| `_Ready` | Called on Godot's `_Ready` (node enters tree). |
| `_Process` | Called on Godot's `_Process`. |

## Restricted Methods

The following methods are **not available** on `Node`:
- `Rpc`, `RpcId`
- `Connect`, `Disconnect`, `EmitSignal`
- `Multiplayer`

### Alternatives

| Need | Use |
|------|-----|
| RPC calls | [`RpcNode`](pages/rpcnode.md) |
| Multiplayer checks | Globals: `IsServer()`, `GetUniqueId()` |
| Events/Signals | [`LuaEvent`](pages/luaevent.md) class |

## See Also

- [Godot Node Class](https://docs.godotengine.org/en/stable/classes/class_node.html)
- [Godot Notifications](https://docs.godotengine.org/en/stable/tutorials/best_practices/godot_notifications.html)