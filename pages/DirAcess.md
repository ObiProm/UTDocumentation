# DirAcess

Available in **`lua/autorun`** scripts of each mod. Provides sandboxed directory operations.

Path schemes and write restrictions: see [Mod paths](pages/mod_paths.md).

---

## Methods

### `DirAcess:DirExists(path): boolean`

Checks whether a directory exists.

#### Parameters:
*   `path` (`string`) — Path using a supported scheme (see [Mod paths](pages/mod_paths.md)).

#### Returns:
*   `boolean` — `true` if the directory exists.

---

### `DirAcess:MakeDir(path)`

Creates a directory recursively (like `MakeDirRecursive`).

#### Parameters:
*   `path` (`string`) — Path. Must use `mod://` or `modsave://`.

---

### `DirAcess:ListDir(path): table`

Lists entries in a directory (files and folders).

#### Parameters:
*   `path` (`string`) — Path using a supported scheme.

#### Returns:
*   `table` — Array of entry names (strings). Empty table if the directory does not exist or cannot be opened.

---

## Example

```lua
if DirAcess:DirExists("mod://Sprites") then
    local files = DirAcess:ListDir("mod://Sprites")
    for i, name in ipairs(files) do
        print(name)
    end
end

DirAcess:MakeDir("modsave://profiles")
```
