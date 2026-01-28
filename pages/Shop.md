# Shop

Manages player currencies and shop-related data.

### How it Works (Currency)
Currencies are defined by a unique string ID (e.g., `"coins"`, `"gems"`). Before a currency can be used, it must be registered using `Shop.RegisterCurrency()`. 

When a player joins the game, the system automatically initializes their balance for all registered currencies with the defined `StartValue`. Player balances are tracked using their `SteamID64` and are automatically saved/loaded between sessions.

## Functions

### `Shop.RegisterCurrency(id, name, iconPath, startValue)`

Registers a new type of currency in the game. This should be called during the game's initialization phase (e.g., in `_Ready` of a main game script).

#### Parameters:
- `id` (`string`) — Unique identifier for the currency (e.g., `"coins"`).
- `name` (`string`) — Display name of the currency (e.g., `"Gold Coins"`).
- `iconPath` (`string`) — Resource path to the currency's icon (e.g., `"res://assets/icons/coin.png"`).
- `startValue` (`int`) — The default starting amount given to new players.

---

### `Shop.GetCurrency(steamId, currencyId)`

Retrieves the current balance of a specific currency for a given player.

#### Parameters:
- `steamId` (`ulong`) — The player's Steam ID 64.
- `currencyId` (`string`) — The unique ID of the currency to check.

#### Returns:
- `long` — The player's current balance of the specified currency. Returns `0` if the currency or player is not found.

---

### `Shop.AddCurrency(player, currencyId, amount)`

Adds currency to player

#### Parameters:
- `player` (`PlayerLobby`) — player object
- `currencyId` (`string`) — The unique ID of the currency to add.
- `amount` (`number`) — Amount of currency

---

### `Shop.AddTower(player, towerId)`

Adds and saves tower

#### Parameters:
- `player` (`PlayerLobby`) — player object
- `towerId` (`string`) — Id of tower