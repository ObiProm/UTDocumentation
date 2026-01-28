### Map Configuration

> Read first: [Loading scenes](pages/loading_scenes.md), [Scene metadata](pages/scene_metadata.md)

Map scenes use the same metadata system as towers. Add fields on the root node in Godot — they become `self.ZombiesPath`, etc. in Lua (available from `_Init`).

#### Required metadata (root node)

| Key | Type | Description |
|-----|------|-------------|
| `ZombiesPath` | `NodePath` | `Path3D` that zombies follow during gameplay |

#### Optional metadata (root node)

| Key | Type | Description |
|-----|------|-------------|
| `OneSpawn` | `Array<NodePath>` | Nodes that spawn only for the first map instance — lighting (`DirectionalLight3D`, `SpotLight3D`), `WorldEnvironment`, global effects |

How to add metadata in Godot: [Scene metadata](pages/scene_metadata.md).