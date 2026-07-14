## Creating setting

To create setting fill [settings Config](pages/settings_config.md)

Also read [build-in settings reference](pages/standard_settings_reference.md)


### Example

Here is how to use settings

```lua
Audio.CreateBus("DJMusic")
Audio.SetBusVolume("DJMusic", SettingsManager.GetSettingValue("dj_volume"))

SettingsManager.OnSettingChanged.Connect(function (settingId, value)
    if settingId == "dj_volume" then
        Audio.SetBusVolume("DJMusic", value)
    end
end)
```