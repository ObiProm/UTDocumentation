## ResourceManager
Allows use of mod resources. All resources load with paths relative to the mod folder.

>**INTERNAL**<br>
>This is used internally — although you're able to use it you probably shouldn't.<br>
>**We recomend to use** `LoadResource(path)` instead of this


---

### `ResourceManager:GetStringResource(path): string`
Loads text data from a file in the mod's directory.

#### Parameters:
- `path` (`string`) — Relative path to the text file.

#### Returns:
- `string` — Content of the loaded file.

---

### `ResourceManager:GetSceneResource(path): PackedScene`
Loads a scene resource (e.g., .tscn file) from the mod's directory.

#### Parameters:
- `path` (`string`) — Relative path to the scene file.

#### Returns:
- `PackedScene` — Loaded scene resource, or `null` if not found.

---

### `ResourceManager:GetTexrure2DResource(path): Texture2D`
Loads a 2D texture resource from the mod's directory.

#### Parameters:
- `path` (`string`) — Relative path to the texture file.

#### Returns:
- `Texture2D` — Loaded texture, or `null` if not found.

---

### `ResourceManager:GetPlaceholderTexture(): Texture2D`
Returns a default placeholder texture (useful for error handling).

#### Returns:
- `Texture2D` — Standard placeholder texture.

---

### `ResourceManager:GetTexrure2DResourceOrPlaceholder(path): Texture2D`
Loads a texture or returns `GetPlaceholderTexture()` if the resource is missing.

#### Parameters:
- `path` (`string`) — Relative path to the texture file.

#### Returns:
- `Texture2D` — Loaded texture or placeholder if missing.

---

### `ResourceManager:GetAudioResource(path): AudioStream`
Loads an audio stream resource (e.g., .wav, .ogg) from the mod's directory.

#### Parameters:
- `path` (`string`) — Relative path to the audio file.

#### Returns:
- `AudioStream` — Loaded audio resource, or `null` if not found.

---

### `ResourceManager:ResourceExists(path): boolean`
Checks if a resource exists at the specified relative path.

#### Parameters:
- `path` (`string`) — Relative path to check.

#### Returns:
- `boolean` — `true` if the resource exists, `false` otherwise.

---

### Example:
```lua
-- Load UI texture with fallback
local logoTex = ResourceManager:GetTexrure2DResourceOrPlaceholder("ui/logo.png")

-- Load configuration data
if ResourceManager:ResourceExists("config/settings.txt") then
    local settings = ResourceManager:GetStringResource("config/settings.txt")
    print("Config loaded: ", settings)
end

```