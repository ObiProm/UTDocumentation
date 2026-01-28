## Setting up scene

> Read first: [Loading scenes](pages/loading_scenes.md), [Scene metadata](pages/scene_metadata.md), [tower config](pages/towersconfig.md)

Tower scenes are ordinary Godot `.scn` files. You configure them with **metadata** on the root node — each key becomes a Lua field on `self` (available from `_Init`).

### Required metadata (root node)

| Key | Type | Description |
|-----|------|-------------|
| `baseLuaClass` | `String` | Your Lua class name from `game.RegisterClass` (e.g. `MyMod_Farm`) |
| `placementArea` | `NodePath` | `Area3D` used to check if the tower fits on the map. Set this area's collision mask to `2` |

### Optional metadata

| Key | Type | Description |
|-----|------|-------------|
| `towerModel` | `NodePath` | 3D model node to rotate when shooting. Required for [`StandardTower`](pages/StandardTower.md) |
| any custom key | any | Becomes `self.YourKey` in Lua — e.g. `Income` (`int`), `farmAudio` (`NodePath`) |

How to add metadata in Godot: [Scene metadata](pages/scene_metadata.md).

### Scene structure

Besides metadata you need nodes in the scene itself:

- **`placementArea`** — `Area3D` (linked via metadata above)
- **`StaticBody3D`** — collision mask `6`, for tower info raycast and upgrade menu. No metadata link needed
- Child nodes referenced by your `NodePath` metadata (audio, labels, models, etc.)

### Example

Metadata on root: `baseLuaClass` = `"MyMod_Farm"`, `Income` = `5`, `farmAudio` → `AudioPlayer`, `incomeLabel` → `UI/IncomeLabel`.

```lua
function Farm:OnTowerPlaced()
    self.farmAudio.Stream = ResourceManager.GetAudioResource("Audio/FarmSound.mp3")
    self.incomeLabel.Text = '+' .. self.Income .. '$'
end
```