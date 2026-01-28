# Loading scenes

Scenes are the main way to bring 3D models, towers, maps, and UI into the game. You create them in Godot, save as `.scn`, and load from Lua.

> New to Godot? A **scene** is a saved tree of nodes (objects). **Instantiating** a scene means creating a copy of that tree and putting it into the game world.

---

## Step 1: Create a scene in Godot

1. In Godot: **Scene → New Scene**.
2. Add nodes (models, collisions, lights, etc.) and save as `.scn` inside your mod folder, e.g. `Scenes/MyTower.scn`.
3. Optionally add [metadata](pages/scene_metadata.md) on nodes — custom fields that become `self.SomeName` in Lua.

For import settings and `.scn` vs `.tscn` see [Importing models](pages/importing_models.md).

---

## Step 2: Load the scene in Lua

Use `LoadResource(path)`. The path is **relative to your mod folder** (same folder structure as in Godot's `res://`).

```lua
local scene = LoadResource("Scenes/MyTower.scn")
```

`LoadResource` returns a `PackedScene` — a template, not yet visible in the world. The only method you need on it is `Instanciate()`.

---

## Step 3: Instantiate and add to the world

```lua
local scene = LoadResource("Scenes/MyTower.scn")
local instance = scene:Instanciate()

game.GetRoot():AddChild(instance)
```

`Instanciate()` creates a real copy of the scene. Every node in that copy is wrapped in a Lua table — you work with `instance` like a normal Lua object (call methods, read fields).

If the root node has metadata `baseLuaClass`, the instance is bound to your Lua class. All other metadata on that node is already available as fields — see [Scene metadata](pages/scene_metadata.md).

---

## Metadata

Metadata is how you pass settings from Godot into Lua without hardcoding values.

You add key/value pairs in the Godot Inspector → **Metadata** section. After instantiate they appear on the Lua table:

```lua
-- In Godot you added: Income (int) = 5
print(self.Income) -- 5, already in _Init
```

Full guide with types, `NodePath`, and a Farm tower example: **[Scene metadata](pages/scene_metadata.md)**.

---

## Notes

- Use `.scn` format for mod scenes when possible — smaller and faster to load.
- `PackedScene` only exposes `Instanciate()` to Lua; you cannot edit the template at runtime.
- After instantiate, nodes are Lua tables, not raw Godot userdata.
- To inspect loaded nodes at runtime, use the [developer console](pages/developer_console.md) → Hierarchy.
