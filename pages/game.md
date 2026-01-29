# Game

The main class for interacting with the native functions.

---

### `game.GetCurrentScene(): Node`

Returns the root node of the currently active scene.

#### Returns:

- `Node` — scene node.

---

### `game.GetRoot(): Node`

Reference to the global scene root.

#### Returns:

- `Node` — root node of the application.

---

### `game.GetUserdataName(object): string`

Returns the type name of a userdata object (e.g., Godot node type).

#### Parameters:

- `object` (`userdata`) — The userdata object.

#### Returns:

- `string` — The type name (e.g., `"Node3D"`).

```lua
local node = game.GetPlayerPacked()
print(game.GetUserdataName(node)) -- "PackedScene"
```

---

### `game.IsNode(obj): boolean`

Checks if the given object is a valid Godot node.

#### Parameters:

- `obj` (`any`) — Object to check.

#### Returns:

- `boolean` — `true` if the object is a node, `false` otherwise.

```lua
local node = game.CreateNode("Node")
print(game.IsNode(node)) -- true
```

---

### `game.GetLanguage(): string`

Returns the current game language setting.

#### Returns:

- `string` — Current language code (e.g., `"en"`, `"ru"`).

```lua
local lang = game.GetLanguage()
print("Current language: " .. lang)
```

---

### `game.CreateNode(className): table`

Creates a new node instance of the specified class.

#### Parameters:

- `className` (`string`) — The name of the class to instantiate (registered Lua class or Godot node type).

#### Returns:

- `table` — A new node instance, wrapped as a Lua object with the appropriate metatable.

```lua
local entity = game.CreateNode("CharacterBody3D")
local customNode = game.CreateNode("MyCustomClass")
```

---

### `game.RegisterClass(className, classTable, baseType?)`

Registers a custom node class that can be instantiated as Godot nodes.

#### Parameters:

- `className` (`string`) — The name of the new class to register.
- `classTable` (`table`) — A Lua table containing methods and properties for the class.
- `baseType` (`string`?) — Optional base Godot node type. Defaults to `"Node"`.

```lua
game.RegisterClass("SuperNode", {
    Talk = function(self, message)
        print("Hello! " .. message)
    end,
    Walk = function(self, distance)
        print("Walking " .. distance .. " units")
    end
}, "Node2D")
```

---

### `game.RegisterSubmodule(className, classTable)`

Registers a submodule that runs independently of game modes. Submodules are loaded for all game modes.

**Read also** [submodules](pages/submodules.md)

#### Parameters:

- `className` (`string`) — Unique name for your submodule.
- `classTable` (`table`) — Lua table containing module methods and properties.

```lua
local test = {}

function test:_Ready()
    local image = game.CreateNode("TextureRect")
    image.Texture = LoadResource("UTIcon.png")
    self:GetParent():AddChild(image)
end

game.RegisterSubmodule("Test", test)
```

---

### `game.BindClass(className, godotNode): table|nil`

Binds an existing Godot node to a registered Lua class.

#### Parameters:

- `className` (`string`) — Name of the registered class.
- `godotNode` (`Node`) — Godot node to bind to the class.

#### Returns:

- `table|nil` — The bound table with class methods, or `nil` if the class is not found.

```lua
local existingNode = someGodotNode
local boundObject = game.BindClass("SuperNode", existingNode)
if boundObject then
    boundObject:Talk("Bound successfully!")
end
```

---

### `game.IsClassRegistered(className): boolean`

Checks if a class has been registered with the game system.

#### Parameters:

- `className` (`string`) — Name of the class to check.

#### Returns:

- `boolean` — `true` if the class is registered, `false` otherwise.

```lua
if game.IsClassRegistered("MyCustomClass") then
    print("Class is available!")
else
    print("Class not found!")
end
```

---

### `game.LoadScene(path): PackedScene`

Loads a scene from the given resource path.

#### Parameters:

- `path` (`string`) — Resource path (e.g., `"Scenes/Game.tscn"`).

#### Returns:

- `PackedScene` — A packed scene ready for instantiation.

```lua
local scene = game.LoadScene("Scenes/Game.tscn")
local instance = scene:Instantiate()
game.GetCurrentScene():AddChild(instance)
```

---

### `game.GetPlayerPacked(): PackedScene`

Returns the default player scene.

#### Returns:

- `PackedScene` — Player scene with `PlayerController` as root.

```lua
local playerScene = game.GetPlayerPacked()
local playerInstance = playerScene:Instantiate()
game.GetCurrentScene():AddChild(playerInstance)
```

---

### `game.GetUIPacked(): PackedScene`

Returns the default UI scene.

#### Returns:

- `PackedScene` — UI scene ready for instantiation.

```lua
local uiScene = game.GetUIPacked()
local uiInstance = uiScene:Instantiate()
game.GetCurrentScene():AddChild(uiInstance)
```

---

### `game.GetMap(map): PackedScene`

Loads a map scene by name or identifier.

#### Parameters:

- `map` (`string`) — Map identifier or name (e.g., `"Level1"`, `"MainMenu"`).

#### Returns:

- `PackedScene` — The packed scene for the specified map.

```lua
local levelScene = game.GetMap("Level1")
game.CurrentScene:ChangeScene(levelScene)
```

---

### `game.CreateNodeWrapper(node): table`

Converts a raw Godot Node into a Lua-wrapped Node with methods and metatable.

#### Parameters:

- `node` (`Node`) — The raw Godot node to wrap.

#### Returns:

- `table` — The wrapped node with Lua class functionality.

> Note: Use this when working with nodes, that was not converted into wrapper by some reason (like base hierarhy elements or because of bug)

```lua
-- When getting something from root, like ServerLobbyManager (its userdata)
local luaNode = game.CreateNodeWrapper(game.GetRoot():GetNode("ServerLobbyManager"))

 -- Now you can add custom fields/functions to this node
luaNode.MyCustomField = "Yay"
```

---

### `game.GetRoomGameScene(room): Node`

Gets the game scene node associated with a room.

#### Parameters:

- `room` (`Room`) — Room object to get the scene for.

#### Returns:

- `Node` — The root node of the room's game scene.

```lua
local room = getCurrentRoom()
local roomScene = game.GetRoomGameScene(room)
roomScene:StartGameplay()
```

---

### `game.GetTowerConfig(towerId): TowerConfig`

Retrieves the configuration data for a specific tower type.

#### Parameters:

- `towerId` (`string`) — Identifier of the tower (e.g., `"BasicTower"`, `"LaserTower"`).

#### Returns:

- `TowerConfig` — Configuration object containing tower properties.

```lua
local config = game.GetTowerConfig("BasicTower")
print("Tower cost: " .. config.cost)
print("Tower damage: " .. config.damage)
```

---

### `game.CreateTower(towerId): Tower`

Creates a new tower instance based on its id.

**Read also** [Tower](pages/tower.md)

#### Parameters:

- `towerId` (`string`) — Identifier of the tower to create.

#### Returns:

- `Tower` — A new tower instance ready for placement.

```lua
local tower = game.CreateTower("Agent")
tower.Position = position
tower:Initialize(GetUniqueId()) -- will bind tower to local player

game.GetCurrentScene():AddChild(tower)
tower.OnTowerPlaced() -- you can skip it, but many towers initializing there
```

---

### `game.CreateEvent(): LuaEvent`

Creates a new Lua event object for event-driven programming. 

**Read also** [LuaEvent](pages/luaevent.md)

#### Returns:

- `LuaEvent` — A new event object that can be subscribed to and fired.

```lua
local myEvent = game.CreateEvent()

-- Subscribe to event
myEvent:Connect(function(someStr, arg2)
    print("Event received:", someStr, arg2)
end)

-- Call event
myEvent:Invoke("Hello from event!", 12)
```

---

### `game.NewStringGUID(): string`

Generates a new unique identifier string (GUID).

#### Returns:

- `string` — A globally unique identifier string.

```lua
local uniqueId = game.NewStringGUID()
print("Generated GUID: " .. uniqueId) -- "a1b2c3d4-e5f6-7890-g1h2-i3j4k5l6m7n8"
```

---

### `game.GetWaveParser(): table`

Returns the wave parser utility for parsing wave configuration data.

#### Returns:

- `table` — Wave parser object with parsing methods.

```lua
local waveParser = game.GetWaveParser()
waveParser.OnEnemySpawnRequested.Connect(self.SpawnZombie, self)
waveParser.OnWaveStarted.Connect(self.StartWave, self)
```

---

### `game.TableToJson(table): string`

Converts a Lua table to a JSON string.

#### Parameters:

- `table` (`table`) — Lua table to convert to JSON.

#### Returns:

- `string` — JSON representation of the table.

```lua
local data = {name = "Player", score = 100, items = {"sword", "shield"}}
local json = game.TableToJson(data)
print(json) -- {"name":"Player","score":100,"items":["sword","shield"]}
```

---

### `game.JsonToTable(json): table`

Converts a JSON string to a Lua table.

#### Parameters:

- `json` (`string`) — JSON string to parse.

#### Returns:

- `table` — Lua table containing the parsed data.

```lua
local json = '{"name":"Player","score":100,"items":["sword","shield"]}'
local data = game.JsonToTable(json)
print(data.name) -- "Player"
print(data.score) -- 100
```

---

### `game.GetTableKeysCount(tbl): integer`

Gets the number of keys in a Lua table.

#### Parameters:

- `tbl` (`table`) — Table to count keys in.

#### Returns:

- `integer` — Number of keys in the table.

```lua
local myTable = {a = 1, b = 2, c = 3}
local count = game.GetTableKeysCount(myTable)
print("Table has " .. count .. " keys") -- "Table has 3 keys"
```

---

### `game.PrintAllLuaTables()`

Prints all paths to nodes, which has binded lua tables. Useful for debugging memory leaks or unexpected behavior.

```lua
-- Call this when debugging to see all registered Lua tables

game.PrintAllLuaTables()

-- Followed by detailed table information
-- /root/@Label@200
-- /root/SomeCustomLuaSystem
-- /root/SomeCustomLuaSystem/Helper
```

---

### `game.PrintTableKeys(tbl)`

Prints all keys of a specific table to the debug log. Useful for inspecting table structure during debugging.

#### Parameters:

- `tbl` (`table`) — Table to inspect.

```lua
local myTable = {name = "Test", value = 42, items = {}}
game.PrintTableKeys(myTable)

-- Output in log: "Table keys: name, value, items"
```