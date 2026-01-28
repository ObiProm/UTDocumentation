# FileAcess

Available in **`lua/autorun`** scripts of each mod. Provides sandboxed file read/write.

Path schemes and write restrictions: see [Mod paths](pages/mod_paths.md).

---

## Methods

### `FileAcess:ReadText(path): string`

Reads a text file.

#### Parameters:
*   `path` (`string`) — Path using a supported scheme (see [Mod paths](pages/mod_paths.md)).

#### Returns:
*   `string` — File contents, or `nil` if the file does not exist or cannot be opened.

---

### `FileAcess:WriteText(path, content)`

Writes text to a file (overwrites existing file).

#### Parameters:
*   `path` (`string`) — Path. Must use `mod://` or `modsave://`.
*   `content` (`string`) — Text to write.

Throws if the path is not writable or the file cannot be opened.

---

### `FileAcess:FileExists(path): boolean`

Checks whether a file exists.

#### Parameters:
*   `path` (`string`) — Path using a supported scheme.

#### Returns:
*   `boolean` — `true` if the file exists.

---

## Example

```lua
local data = FileAcess:ReadText("mod://config/extra.json")
if data then
    print("Loaded")
end

FileAcess:WriteText("modsave://progress.txt", "level=5")
```
