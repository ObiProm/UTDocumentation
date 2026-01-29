## Loading scenes with Lua

Use the global `LoadResource(path)` function to load scenes in your mod scripts:

```lua
-- Load a scene from the mod's resources
local scene = LoadResource("Scenes/MyScene.scn")

-- Instantiate the scene (returns a Lua-wrapped node)
local instance = scene:Instanciate()

-- Add to the game world
game.GetRoot():AddChild(instance)
```

### Metadata

All metadata and custom properties added in the Godot editor will be available in the Lua node table (you can check it in [developer console](pages/developer_console.md), in hierarchy tab)

But we have some important details:
- `NodePath` properties will automatically resolve to actual node references
- Property with name `baseLuaClass`(string) will bind node to this class if it was registered by `game.RegisterClass(className, table, baseClass)`

**Important Notes:**
- `LoadResource()` returns a `PackedScene` object
- The `PackedScene` only has the `Instanciate()` method available
- When instantiated, all nodes are automatically wrapped in Lua tables (not userdata)
