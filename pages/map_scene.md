### Map Configuration

> Please, read [Loading scenes](pages/loading_scenes.md) first

Maps have special metadata fields that control gameplay behavior. 

#### Required Metadata Fields

- **`ZombiesPath`** (`NodePath`): **Required** - The path that zombies will follow during gameplay. This must be a valid `Path3D` node.

#### Optional Metadata Fields

- **`OneSpawn`** (`Array<NodePath>`): Elements that should only spawn for the first instance of the map. This is recommended for:
  - Lighting nodes (`DirectionalLight3D`, `SpotLight3D`, etc.)
  - `WorldEnvironment` nodes
  - Global effects that shouldn't duplicate