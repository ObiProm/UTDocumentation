## LuaEvent
Represents a custom event system for creating and managing events. LuaEvent instances are created using `game.CreateEvent()`.

---

### `LuaEvent:Connect(callback, table?)`
Connects a callback function to the event. The callback will be executed when the event is invoked.

#### Parameters:
- `callback` (`function`) — Function to be called when the event is triggered.
- `table` (`table?`) — Optional table to use as the context (`self`) when calling the callback.

---

### `LuaEvent:Disconnect(callback, table?)`
Disconnects a previously connected callback function from the event.

#### Parameters:
- `callback` (`function`) — The exact callback function that was connected.
- `table` (`table?`) — Optional context table that was used when connecting the callback.

---

### `LuaEvent:Invoke(...)`
Invokes the event, triggering all connected callbacks with the provided arguments.

#### Parameters:
- `...` (`any`) — Variable arguments that will be passed to all connected callbacks.

---

### Example:
```lua  
-- Create event for player damage  
local OnPlayerDamaged = game.CreateEvent()  

-- 1. Connect named function  
local function LogDamage(amount, source)  
    print(string.format("Took %d damage from %s", amount, source))  
end  
OnPlayerDamaged:Connect(LogDamage)  

-- 2. Connect anonymous function (store reference!)  
local healthBarUpdater  
healthBarUpdater = function(amount)  
    print("Updating health bar: -" .. amount)  
end  
OnPlayerDamaged:Connect(healthBarUpdater)  

-- 3. Connect method with context  
local Player = {  
    health = 100,  
    OnDamage = function(self, amount)  
        self.health = self.health - amount  
        print("Player health: " .. self.health)  
    end  
}  
OnPlayerDamaged:Connect(Player.OnDamage, Player)  

-- Trigger the event  
OnPlayerDamaged:Invoke(15, "Grenade")  
-- Output:  
-- Took 15 damage from Grenade  
-- Updating health bar: -15  
-- Player health: 85  

-- Disconnect properly  
OnPlayerDamaged:Disconnect(LogDamage)          -- Disconnect named function  
OnPlayerDamaged:Disconnect(healthBarUpdater)   -- Disconnect stored anonymous function  
OnPlayerDamaged:Disconnect(Player.OnDamage, Player)  -- Disconnect method  

-- Only disconnected callbacks won't trigger  
OnPlayerDamaged:Invoke(10, "Pistol")  
-- Output: (only Player health updates)  
-- Player health: 75  
```  