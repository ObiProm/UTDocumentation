# UpgradeMenuUI

UI control for the tower upgrade menu.

To customize the menu (buttons, open/close hooks, blocking open) use virtual functions on [`Tower`](pages/tower.md): `PreUpgradeMenuOpen`, `OnUpgradeMenuOpened`, `OnUpgradeMenuClosed`, `PopulateUpgradeMenuButtons`, `PreProcessUpgrade`, `TowerUpgradePrecessed`.

---

## Methods

### `UpgradeMenuUI:SetTower(tower)`

Selects a tower and opens the menu for it.

Closes the menu for the previously selected tower, calls `PreUpgradeMenuOpen` on the new tower, and if allowed — rebuilds the menu content. If `PreUpgradeMenuOpen` returns `false`, the menu stays hidden (the previous tower's menu is already closed).

#### Parameters:
*   `tower` (`Tower`) — The tower to display.

---

### `UpgradeMenuUI:SetUpgradeIcon(texture)`

Sets the icon in the bottom upgrade detail panel.

#### Parameters:
*   `texture` (`Texture2D`) — Icon texture.

---

### `UpgradeMenuUI:SetUpgradeNameText(text)`

Sets the upgrade name label in the bottom panel.

#### Parameters:
*   `text` (`string`) — Display text.

---

### `UpgradeMenuUI:SetUpgradeDescriptionText(text)`

Sets the upgrade description label in the bottom panel.

#### Parameters:
*   `text` (`string`) — Display text.

---

### `UpgradeMenuUI:SetUpgradeButtonText(text)`

Sets the text of the main upgrade action button in the bottom panel.

#### Parameters:
*   `text` (`string`) — Button label.

---

### `UpgradeMenuUI:SetUpgradeButtonCallback(closure)`

Sets a Lua callback invoked when the main upgrade button is pressed.

#### Parameters:
*   `closure` (`function`) — Lua function called with `upgradeMenuUI` as argument.

---

### `UpgradeMenuUI:SetDisabledUpgrade(disabled)`

Shows or hides the overlay that blocks the bottom upgrade button.

#### Parameters:
*   `disabled` (`boolean`) — `true` to show the disabled overlay.

---

### `UpgradeMenuUI:Reset()`

Resets the bottom upgrade panel to defaults: placeholder icon, `"Upgrade description"` text, `"Upgrade"` button text, callback cleared, disabled overlay hidden.

---

## Customization

All menu customization is done through [`Tower`](pages/tower.md) virtual functions — especially `PopulateUpgradeMenuButtons`, where you can call `Set*` methods on the `upgradeMenu` argument:

```lua
function MyTower:PopulateUpgradeMenuButtons(upgradeMenu, additionalButtonsContainer, bottomIconContainer)
    upgradeMenu:SetUpgradeNameText("Special ability")
    upgradeMenu:SetUpgradeDescriptionText("Activate once per wave")
    upgradeMenu:SetUpgradeButtonText("Activate")
    upgradeMenu:SetUpgradeButtonCallback(function(menu)
        print("Ability used!")
        menu:SetDisabledUpgrade(true)
    end)
end
```
