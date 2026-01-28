# Mod paths

`FileAcess` and `DirAcess` (available in `lua/autorun` scripts) use special path prefixes to access mod files safely. See [FileAcess](pages/FileAcess.md) and [DirAcess](pages/DirAcess.md) for API.

> **Note:** the names are spelled `FileAcess` and `DirAcess` (not "Access") — use them exactly as shown.

---

## Path schemes

| Prefix | Read | Write | Description |
|--------|------|-------|-------------|
| `mod://` | yes | yes | Files inside the current mod folder |
| `modsave://` | yes | yes | Per-mod save folder: `user://mod_saves/{ModId}/` |
| `user://` | yes | no | Godot user data directory (read only through this API) |
| plain path | yes | no | Resolved as-is (read only) |
| `res://` | — | — | **Forbidden** — throws an error |

**Write access is only available through `mod://` and `modsave://`.** Any write attempt with another prefix will throw an error.

---

## `mod://`

Points to the root folder of the current mod (the folder containing `config.json`).

```lua
FileAcess:ReadText("mod://data/config.json")
FileAcess:WriteText("mod://data/cache.txt", "hello")
```

Use for mod-owned data that ships with the mod or can be edited at runtime inside the mod folder.

---

## `modsave://`

Points to `user://mod_saves/{ModId}/` — a separate folder per mod in the player's user data. Created automatically on first write.

```lua
DirAcess:MakeDir("modsave://profiles")
FileAcess:WriteText("modsave://profiles/player1.txt", "score=100")
```

Use for player progress, settings, and other persistent data that should survive between game sessions.

---

## `user://`

Standard Godot user data path. Can be used for **reading** through `FileAcess` / `DirAcess`, but **writing is not allowed** — use `modsave://` instead.

---

## Security

*   `res://` (game resources) cannot be accessed — mods cannot read or overwrite game files through this API.
*   Path traversal (`..`) is blocked — you cannot escape outside the allowed base directory.

---

## Examples

```lua
-- Read from mod folder
local json = FileAcess:ReadText("mod://data/settings.json")

-- Write save data
DirAcess:MakeDir("modsave://saves")
FileAcess:WriteText("modsave://saves/slot1.json", "{}")

-- List mod files
local files = DirAcess:ListDir("mod://Sprites")
```

For loading game resources (textures, scenes) prefer [`LoadResource`](pages/globals.md) / [`ResourceManager`](pages/resourcemanager.md).
