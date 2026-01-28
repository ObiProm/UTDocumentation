# Scene metadata

Metadata lets you attach custom settings to a node directly in the Godot editor — without writing code. When a scene is loaded, these values are copied into the Lua table of that node. You read and use them as ordinary fields: `self.Income`, `self.farmAudio`, and so on.

## How it works
1. Open a `.scn` scene in Godot and select a node.
2. In the Inspector (right panel), scroll down and add metadata: a key (name), a type, and a value.
3. When the game loads the scene, each metadata entry becomes a field on the Lua table bound to that node.
4. In Lua you use `self.KeyName` — the same name you typed as the metadata key.

**Example:** You added metadata `Income` = `5` (type `int`) on the root node. In Lua:
```lua
print(self.Income) -- 5
```
No extra loading step — the value is already on `self`.

## When are fields available?
Metadata fields are available starting from `_Init` — right after the node is created, before `_Ready` and before any gameplay events like `OnTowerPlaced`.

That means you can safely use metadata in `_Init`:
```lua
function Farm:_Init()
    print("Income per tick:", self.Income)
end
```
You do not need to wait for `_Ready` or `OnTowerPlaced` to read metadata values.

## How to add metadata in Godot
1. Open your scene (`.scn`) in Godot.
2. In the Scene dock (left), click the node you want to configure — usually the root node of the tower or map.
3. In the Inspector (right), scroll to the very bottom until you see the **Metadata** section.
4. Click **Add Metadata**.
5. Choose the type (`String`, `int`, `float`, `bool`, `NodePath`, etc.).
6. Enter the key — this becomes the field name in Lua (`Income`, `farmAudio`, `placementArea`, …).
7. Set the value.
8. Save the scene. The metadata is stored inside the `.scn` file.

## Types and what you get in Lua

| Godot metadata type | Lua type | Example key | Example value | In Lua |
| :--- | :--- | :--- | :--- | :--- |
| **String** | string | DisplayName | "Gold Farm" | `self.DisplayName` |
| **int** | number | Income | 5 | `self.Income` |
| **float** | number | GrowSpeed | 1.5 | `self.GrowSpeed` |
| **bool** | boolean | IsActive | true | `self.IsActive` |
| **NodePath** | node (table) | farmAudio | *path to node* | `self.farmAudio` |

### `NodePath` — link to another node in the scene
If the type is `NodePath`, Godot stores a path like `AudioPlayer` or `UI/IncomeLabel`. The game resolves it automatically: in Lua you get a reference to that child node, not a string.

**Example:** You set metadata `farmAudio` (`NodePath`) → `AudioPlayer`. In Lua `self.farmAudio` is the audio node:
```lua
self.farmAudio.Stream = ResourceManager.GetAudioResource("Audio/FarmSound.mp3")
```
You pick the path in Godot by clicking the picker next to the value field and selecting a node from the scene tree.

## Special metadata: `baseLuaClass`

`baseLuaClass` (`String`) is used to **bind your Lua class to the node**. 

**Important:** Every node gets a Lua table automatically when loaded, and metadata works without `baseLuaClass`. You can call standard Godot node methods and read metadata fields even without it.

However, if you want to add **custom behavior** (methods like `_Init`, `OnTowerPlaced`, etc.), you need to tell the game which Lua class to use. That's what `baseLuaClass` does.

**How to use it:**
1. Create and register your Lua class via `game.RegisterClass("MyMod_Farm", Farm, "Tower")`.
2. Add metadata `baseLuaClass` (type: `String`) on the **root node** of your scene.
3. Set the value to your registered class name (e.g., `MyMod_Farm`).

Without `baseLuaClass`, the node still has a Lua table and metadata, but it won't execute your custom methods.

## Full example: Farm tower

**Scene structure:**
```text
Farm (root)          ← metadata lives here
├── AudioPlayer
└── UI
    └── IncomeLabel
```

**Metadata on root node:**
| Key | Type | Value |
| **baseLuaClass** | String | MyMod_Farm |
| Income | int | 5 |
| farmAudio | NodePath | AudioPlayer |
| incomeLabel | NodePath | UI/IncomeLabel |

**Lua implementation:**
```lua
local Farm = {}

function Farm:_Init()
    -- Metadata is already on self
    print("This farm earns", self.Income, "per tick")
end

function Farm:OnTowerPlaced()
    self.farmAudio.Stream = ResourceManager.GetAudioResource("Audio/FarmSound.mp3")
    self.incomeLabel.Text = '+' .. self.Income .. '$'
end

game.RegisterClass("MyMod_Farm", Farm, "Tower")
```

**What happens:**
- `self.Income` came from metadata (int → number).
- `self.farmAudio` and `self.incomeLabel` came from `NodePath` metadata and point to child nodes.
- `baseLuaClass` tells the game to use the `Farm` class for this node, so `_Init` and `OnTowerPlaced` are called.

## Debugging
You can inspect metadata fields on a live node in the [developer console](pages/developer_console.md) → **Hierarchy** tab: select a node and check its Lua table on the right.

## See also
- [Loading scenes](pages/loading_scenes.md) — how to load and spawn `.scn` files
- [Setting up tower scene](pages/tower_scene.md) — required metadata for towers
- [Setting up map scene](pages/map_scene.md) — required metadata for maps
