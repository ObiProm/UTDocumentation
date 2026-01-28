# StandardTower

Inherits from: [`Tower`](pages/tower.md) → [`GameEntity`](pages/GameEntity.md) → `Node3D`

A standard tower implementation that automatically detects zombies in its range, selects targets based on a configurable priority, and deals damage over time.

## Fields

<div class="markdownTable">

| Field | Type | Access | Description |
|-------|------|--------|-------------|
| `Range` | `number` | get/set | The detection radius of the tower. Updating this automatically resizes the internal collision shape. |
| `Damage` | `integer` | get/set | The amount of damage dealt per shot. Default: `2`. |
| `ShootTime` | `number` | get/set | The cooldown time in seconds between shots. Default: `2.0`. |
| `IsAvalibleShot` | `boolean` | get | `true` if the tower's cooldown has finished and it is ready to fire. |
| `DamageDealed` | `integer` | get | Total damage dealt by this tower since it was placed. |
| `CurrentTarget` | `TargetPriority` | get | The current targeting priority. Possible values: `First`, `Last`, `Strongest`, `Weakest`. |
| `Zombies` | `table<Zombie>` | get | Here you can read/add zombies |
| `UseModelFront` | `boolean` | get/set | Passed to Godot's `LookAt` as `useModelFront`. Controls which axis of the model is treated as "forward" when the tower rotates toward a target. Default: `false`. See [Godot docs](https://docs.godotengine.org/en/stable/classes/class_node3d.html#class-node3d-method-look-at). |

</div>

## Methods

### `StandardTower:InitializeStandardTower()`

Starts tower combat logic after placement. Called automatically from `OnTowerPlaced`, but you can call it manually if you override placement logic.

What it does:
*   Resolves `towerModel` from the Lua table and stores it for rotation.
*   Creates and starts the shoot cooldown timer.
*   Enables the range `Area3D` collider and configures collision layers/masks.
*   Subscribes to `BodyEntered` / `BodyExited` on the range collider to track zombies in `Zombies`.

You must call this (or call `OnTowerPlaced` which calls it) for the tower to detect and shoot enemies.

* * *

### `StandardTower:RpcChangeTarget(newTarget)`

Changes the tower's targeting priority. This is typically triggered by the UI button in the upgrade menu, but can be called manually. If calls on server changes this at all clients.

#### Parameters:
*   `newTarget` (`integer`) — The new priority as an integer (`0` = First, `1` = Last, `2` = Strongest, `3` = Weakest).

* * *

### `StandardTower:LoadModel(node)`

By default `StandardTower:InitializeStandardTower()` calls `StandardTower:LoadModel(self.towerModel)`, but i you want to do it later you can use this function

#### Parameters:
*   `node` (`Node`) — node to become a model

* * *

### `StandardTower:RpcChangeTarget(newTarget)`

Changes the tower's targeting priority. This is typically triggered by the UI button in the upgrade menu, but can be called manually. If calls on server changes this at all clients.

#### Parameters:
*   `newTarget` (`integer`) — The new priority as an integer (`0` = First, `1` = Last, `2` = Strongest, `3` = Weakest).

* * *

### `StandardTower:GetTargets(count, targetPriority): table<Zombie>`

Gets multiple targets by TargetPriority

#### Parameters:
*   `count` (`number`) — how much zombies will be at returned value
*   `targetPriority` (`enum`) — Targeting priority. Possible values: `First`, `Last`, `Strongest`, `Weakest`.

#### Returns:
*   ` table<Zombie>` — zobmie table

* * *

## Virtual functions

Here you can see functions which are called on specific events. You can define these in your tower's Lua table to customize behavior.

| Function | Parameters | Description |
|----------|------------|-------------|
| `ProcessShot` | `target` (`Zombie`) | If defined in Lua, **overrides** the default shooting logic. Called when a target is in range and the tower is ready to shoot. Use this for custom projectiles or effects. |
| `OnShot` | `target` (`Zombie`) | Called every time the tower fires (after the cooldown), regardless of whether `ProcessShot` is overridden. |
| `OnPreviewPlaced` | - | Called when the tower is placed in preview mode. Automatically spawns a visual range indicator. |
| `OnUpgradeMenuOpened` | `upgradeMenuUI` (`UpgradeMenuUI`) | Called when the tower is selected in the world. Automatically spawns a visual range indicator. |
| `OnUpgradeMenuClosed` | `upgradeMenuUI` (`UpgradeMenuUI`) | Called when the tower is deselected. Automatically removes the visual range indicator. |
| `PopulateUpgradeMenuButtons` | `upgradeMenu` (`UpgradeMenuUI`), `additionalButtonsContainer` (`Control`), `bottomIconContainer` (`Control`) | Called to populate the upgrade menu. This implementation adds a "Target Priority" toggle button to `additionalButtonsContainer` and a "Damage Dealt" label to `bottomIconContainer`. |
| `OnZombieEnteredRange` | `zombie` (`Zombie`) | Called when zombie enters range of tower. |
| `OnZombieExitedRange` | `zombie` (`Zombie`) | Called when zombie exits range of tower. |
