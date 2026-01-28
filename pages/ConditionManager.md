# ConditionManager

Creates, checks, syncs all conditions. This system is created for shop, but you can use it for your goals

---


### `ConditionManager.CreateCondition(name, func): void`

Creates condition that can be checked by ConditionManager.IsConditionComplete(name). First at `func` arg will be `senderId` (PlayerLobby.PeerID)

#### Parameters:

- `name` (`string`) — condition name
- `func` (`function`) — condition function. Must returns `boolean`

---


### `ConditionManager.IsConditionComplete(name, args): boolean`

Checks condtion which was created by ConditionManager.CreateCondition(name, func)

#### Parameters:

- `name` (`string`) — condition name
- `args` (`...`) — condition args

#### Parameters:

- `is_completed` (`boolean`) — is condition competed

---

### `ConditionManager.IsConditionCompleteServer(func, name, args): void`

Checks condtion **AT SERVER**. This is async func, because of that you need to player `func`, it will be called after response. First arg will be `boolean`, don't use it in tables (first arg at table's func is `self`)

#### Parameters:

- `func` (`function`) — function which be called on server response
- `name` (`string`) — condition name
- `args` (`...`) — condition args

```lua
--- Created at server
ConditionServer.CreateCondition("My_condition", function (sender)
    return ConditionTable[sender.SteamID64]
end)

--- Call at client
ConditionServer.IsConditionCompleteServer(function (res)
    print("Result is", res)
end, "My_condition")

```