<h2>PlayerController</h2>

Noclip camera, using to give player access to fly around the world

<h3>Fields</h3>


<div class="markdownTable">

| Field                        | Type                            | Access   | Description |
|------------------------------|---------------------------------|----------|-------------|
| `Player`                     | `PlayerLobby`                   | get/set  | Sets or gets player, which was binded to this player controller. |
| `IsLocalPlayer`              | `boolean`                       | get      | Returns is current PlayerController binded to local player. |
| `CurrentSpeed`               | `number`                        | get      | Returns movement speed of player |
| `TowerPlacementManager`      | `TowerPlacementManager`         | get      | Contains `TowerPlacementManager`, you also can get that using `game.GetRoomGameScene(room).TowerPlacementManager` |

</div>