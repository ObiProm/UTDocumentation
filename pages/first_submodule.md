# First submodule

Now you know basics, and you can write something usefull. Like submodule.

A submodule is a component that loads automatically when the game starts and works across all gamemodes

Create `lua/autorun/PlaytimeCounter.lua`:
```lua
local PlaytimeCounter = {}
local seconds = 0

function PlaytimeCounter:_Ready()
    self.label = game.CreateNode("Label")
    self.label.Text = "Playtime: 00:00:00"
    self.label.Position = Vector2(20, 20)
    self.label.AddThemeFontSizeOverride("font_size", 24)
    game.GetRoot():AddChild(self.label)
end

function PlaytimeCounter:_Process(delta)
    if delta > 1 then return end
    seconds = seconds + delta
    if seconds % 1 < delta then
        self:UpdateLabel()
    end
end

function PlaytimeCounter:UpdateLabel()
    local h = math.floor(seconds / 3600)
    local m = math.floor((seconds % 3600) / 60)
    local s = math.floor(seconds % 60)
    self.label.Text = string.format("Playtime: %02d:%02d:%02d", h, m, s)
end

game.RegisterSubmodule("PlaytimeCounter", PlaytimeCounter)
```