## Creating setting

To create setting fill [settings Config](pages/settings_config.md)




```lua
Audio.CreateBus("DJMusic")
Audio.SetBusVolume("DJMusic", SettingsManager.GetSettingValue("dj_volume"))

SettingsManager.OnSettingChanged.Connect(function (settingId, value)
    if settingId == "dj_volume" then
        Audio.SetBusVolume("DJMusic", value)
    end
end)
```