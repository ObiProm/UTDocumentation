# TowerPlacementManager

Controls tower placement.

---

### `TowerPlacementManager.RegisterInventoryButton(button, index)`

Binds to button activation of placement.

#### Parameters:

- `button` (`BaseButton`) — button to bind.
- `index` (`number`) — what index of inventory get (starts from 0).

---

## Fields

| Field | Type |
|-------|------|
| `EnableDefaultPlacementSyncronizer` | `boolean` |
| `EnableDefaultPlacementChecker` | `boolean` |
| `ProcessPlacementFunction` | `function` |
| `ClientPreProcessPlacementFunction` | `function` |
| `EconomyManager` | `EconomyManager` |

---

## Events

| Event | Parameters |
|-------|------------|
| `OnPlacementConfirmed` | `string towerId`, `Vector3 position` |
| `OnPlacementStarted` | `string towerId` |
| `OnPlacementEnded` | `string towerId` |
| `OnPlacementModeExited` | `string towerId` |
| `OnTowerPlaced` | `Tower towerObj`, `string towerId`, `Vector3 position` |