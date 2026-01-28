# TowerPlacementManager

Controls tower placement.

---

## Fields

| Field | Type | Info |
|-------|------|------------|
| `EnableDefaultPlacementSyncronizer` | `boolean` | If true will spawn tower at all clients after server checked is tower at valid position (default if true) |
| `EnableDefaultPlacementChecker` | `boolean` | If true will check is tower's `placementArea` overlaps blocked areas (default if true) |
| `ProcessPlacementFunction` | `function(string towerId, Vector3 position, Vector3 rotation, Node3D towerPreview)` | calls at **client** when client tries to place a tower |
| `ClientPreProcessPlacementFunction` | `function(number senderId, string towerId, Vector3 position, Vector3 rotation)` | calls at **server** when client tries to place a tower |
| `EconomyManager` | `EconomyManager` | - |

---

### `TowerPlacementManager.RegisterInventoryButton(button, index)`

Binds to button activation of placement.

#### Parameters:

- `button` (`BaseButton`) — button to bind.
- `index` (`number`) — what index of inventory get (starts from 0).

---

## Events

| Event | Parameters |
|-------|------------|
| `OnPlacementConfirmed` | `string towerId`, `Vector3 position` |
| `OnPlacementStarted` | `string towerId` |
| `OnPlacementEnded` | `string towerId` |
| `OnPlacementModeExited` | `string towerId` |
| `OnTowerPlaced` | `Tower towerObj`, `string towerId`, `Vector3 position` |