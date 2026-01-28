# EconomyManager

Manages the in-game economy, including multiple currency types, player balances, and purchase processing. It operates on a server-authoritative model, automatically syncing balances and UI elements to clients.

## Methods

### `EconomyManager:RegisterCurrency(currencyType, symbol, defaultAmount)`

Registers a new currency type in the economy. If called on the server, it automatically initializes the default amount for all currently connected players.

#### Parameters:
*   `currencyType` (`string`) — Unique identifier for the currency (e.g., `"Gold"`, `"Wood"`).
*   `symbol` (`string`) — Visual symbol or suffix for the currency (e.g., `"G"`, `" kg"`).
*   `defaultAmount` (`number`) — The starting amount given to players when this currency is registered.

* * *

### `EconomyManager:AddCurrency(playerId, currencyType, amount): boolean`

Adds a specific amount of currency to a player's balance. **Server only.**

#### Parameters:
*   `playerId` (`number`) — The PeerID of the player.
*   `currencyType` (`string`) — The currency to add.
*   `amount` (`number`) — The amount to add.

#### Returns:
*   `boolean` — `true` if successful, `false` if called on the client or the currency type doesn't exist.

* * *

### `EconomyManager:AddCurrencyRequest(currencyType, amount)`

Sends a request to the server to add currency to the local player. Used for client-side triggers (e.g., picking up an item).

#### Parameters:
*   `currencyType` (`string`) — The currency to add.
*   `amount` (`number`) — The amount to add.

* * *

### `EconomyManager:RemoveCurrency(playerId, currencyType, amount)`

Removes a specific amount of currency from a player's balance. **Server only.** Note: This does not check if the player has enough funds; use `CanAfford` first.

#### Parameters:
*   `playerId` (`number`) — The PeerID of the player.
*   `currencyType` (`string`) — The currency to remove.
*   `amount` (`number`) — The amount to remove.

* * *

### `EconomyManager:CanAfford(currencyType, amount, playerId): boolean`

Checks if a specific player has enough of a certain currency.

#### Parameters:
*   `currencyType` (`string`) — The currency to check.
*   `amount` (`number`) — The required amount.
*   `playerId` (`number`) — The PeerID of the player.

#### Returns:
*   `boolean` — `true` if the player has enough funds.

* * *

### `EconomyManager:CanAfford(currencyType, amount): boolean`

Checks if the local player has enough of a certain currency.

#### Parameters:
*   `currencyType` (`string`) — The currency to check.
*   `amount` (`number`) — The required amount.

#### Returns:
*   `boolean` — `true` if the local player has enough funds.

* * *

### `EconomyManager:GetBalance(currencyType, playerId): number`

Retrieves the current balance of a specific currency for a player.

#### Parameters:
*   `currencyType` (`string`) — The currency to check.
*   `playerId` (`number`) — The PeerID of the player.

#### Returns:
*   `number` — The current balance, or `0` if the player or currency doesn't exist.

* * *

### `EconomyManager:RegisterUILabel(currencyType, label)`

Registers a UI `Label` node to automatically display and update the local player's balance for a specific currency whenever it changes.

#### Parameters:
*   `currencyType` (`string`) — The currency this label should display.
*   `label` (`Label`) — The UI Label node to update.

* * *

### `EconomyManager:SendRequestPurchase(currencyType, amount)`

Sends a purchase request to the server. The server will check if the local player can afford it, deduct the funds, and trigger the appropriate success/fail events.

#### Parameters:
*   `currencyType` (`string`) — The currency to spend.
*   `amount` (`number`) — The amount to spend.

* * *

### `EconomyManager:ServerProcessPurchase(currencyType, amount, playerId): boolean`

Processes a purchase for a specific player. **Server only.** Checks if the player can afford the amount, deducts it, and notifies the client.

#### Parameters:
*   `currencyType` (`string`) — The currency to spend.
*   `amount` (`number`) — The amount to spend.
*   `playerId` (`number`) — The PeerID of the player making the purchase.

#### Returns:
*   `boolean` — `true` if the purchase was successful, `false` if insufficient funds.

* * *

### Events

<div class="markdownTable">

| Event | Parameters | Description |
|-------|------------|-------------|
| `PurchaseSuccess` | `currencyType` (`string`), `amount` (`number`) | Invoked on the client when a local purchase request is successfully processed by the server. |
| `PurchaseFailed` | `error` (`string`) | Invoked on the client when a local purchase request fails (e.g., "Insufficient funds"). |
| `OnServerPurchaseSuccess` | `peerID` (`number`), `currencyType` (`string`), `amount` (`number`) | Invoked on the server when any player successfully completes a purchase. |

</div>