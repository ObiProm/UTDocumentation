## SettingsManager

Provides access to game settings system. Allows reading and modifying settings values, and listening to setting changes.

> Read also [standard settings reference](pages/standard_settings_reference.md)


## Functions

### `SettingsManager.OnSettingChanged` -> `Signal`

Signal emitted when any setting value is changed.

**Signal Parameters:**
- `settingId` (`string`) — The ID of the setting that was changed
- `value` (`any`) — The new value of the setting

### `SettingsManager.GetSettingValue(settingId)` -> `any`

Retrieves the current value of a setting.

**Parameters:**
- `settingId` (`string`) — The unique identifier of the setting

**Returns:**
- `any` — The current value of the setting (type depends on setting configuration)

**Example:**
```lua
local volume = SettingsManager.GetSettingValue("audio_master")
print("Current volume:", volume)

local fullscreen = SettingsManager.GetSettingValue("graphics_fullscreen")
print("Fullscreen enabled:", fullscreen)
```

### `SettingsManager.SetSettingValue(settingId, value)` -> `void`

Changes the value of a setting. Triggers the `OnSettingChanged` signal.

**Parameters:**
- `settingId` (`string`) — The unique identifier of the setting
- `value` (`any`) — The new value to set (must match the setting's expected type)

**Example:**
```lua
-- Change audio volume
SettingsManager.SetSettingValue("audio_master", 0.75)

-- Toggle fullscreen
SettingsManager.SetSettingValue("graphics_fullscreen", true)

-- Change VSync state
SettingsManager.SetSettingValue("graphics_vsync", "high")
```