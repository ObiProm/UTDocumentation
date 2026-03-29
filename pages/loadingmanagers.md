# Loading managers

Loading managers created to initialize gamemodes. After lobby admin pressed `Start game`, the game creates a node in the root with class  `RoomGameScene` (also accessible via `game.GetRoomGameScene(room)`). This node is named `game_{room name}` and serves as the root for all gameplay systems of that room. So hierarchy after that looks like

```
Root
├── Some game managers
├── game_room_0        ← RoomGameScene instance for room "room_0"
└── game_room_1        ← RoomGameScene instance for room "room_1"
```

After that game checks selected gamemode and reading its [config](pages/gamemodesconfig.lua) and reads its `LoadingManagerScript` field.It then instantiates that manager via `game.CreateNode(LoadingManagerScript)` as a child of the corresponding `RoomGameScene`. Most often, it is inherited from the built-in LoadingManager, which already has blanks to check how many players are in the lobby and whether it is possible to start the game.

Lets look how to write it
