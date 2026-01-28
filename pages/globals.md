## Globals

### `print(...)`

Prints a message to the console.

### `printError(...)`

Prints an error message (displayed in red).

### `printWarning(...)`

Prints a warning message (displayed in yellow).

---

### `Vector3(X, Y, Z): Vector3`

Creates a 3D vector.

#### Parameters:

- `X`, `Y`, `Z` (`number`) — Coordinates.

#### Returns:

- `Vector3` — A new 3D vector.

---

### `Vector2(X, Y, Z): Vector2`

Creates a 2D vector.

#### Parameters:

- `X`, `Y` (`number`) — Coordinates.

#### Returns:

- `Vector2` — A new 2D vector.

---

### `IsLocalForRoom(room): boolean`

Checks whether the current local player is a member of the room.

#### Parameters:

- `room` (`Room`) — Checks for this room.

#### Returns:

- `boolean` — `true` if the current local player is a member of the room.

---

### `LocalPlayer(): PlayerLobby`

Returns a local player object.

#### Returns:

- `PlayerLobby` — player object.

---

### `IsServer(): boolean`

Checks if the current instance is running as a server.

#### Returns:

- `boolean` — `true` if the application is a server.

---

### `GetUniqueId(): number`

Returns unique ID.

#### Returns:

- `number` — unique ID of current running instace (1 = server)

---

### `LoadResource(path): any`

Loads resource from given path. Internally uses `ResourceManager`.

#### Parameters:

- `path` (`string`) — path to resource.

#### Returns:

- `any` — any resource file.