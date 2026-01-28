# Events

Events are a fundamental part of game development. They allow different parts of your mod (or the game itself) to communicate without being tightly coupled. Instead of one script directly calling functions in another, they send events, and any interested script can listen and react.

In Uninfected Tower modding, events are handled via the `LuaEvent` class. 

## Native Events (Godot Signals)

If you are familiar with Godot, you know it uses **Signals** (like `pressed` for buttons or `body_entered` for collisions). 

In our Lua API, **all native Godot signals are automatically converted into `LuaEvent` objects** (Names conterts to **PascalCase**). This means you can interact with built-in Godot nodes using the exact same event system as your custom Lua events.

### Example: Native Collision Event
Let's create an `Area3D` and listen to its native collision signal:

```lua
local area = game.CreateNode("Area3D")

-- The native 'BodyEntered' signal is automatically a LuaEvent!
area.BodyEntered:Connect(function(body)
    print("Something entered the area: " .. body:GetName())
end)
```
Because native signals are converted to `LuaEvent`, you use the same `:Connect()` and `:Disconnect()` methods for both Godot's built-in signals and your own custom events.

## Creating Custom Events (`LuaEvent`)

While native signals are great for Godot nodes, you often need to create your own events to communicate between your custom Lua classes. 

To create a custom event, use `game.CreateEvent()`.

```lua
-- Create a custom event for when the player takes damage
local OnPlayerDamaged = game.CreateEvent()
```

### Invoking an Event
To trigger the event and notify all listeners, use `:Invoke(...)`. You can pass any number of arguments.

```lua
-- Trigger the event, passing damage amount and source
OnPlayerDamaged:Invoke(15, "Grenade")
```

### Connecting to an Event
There are two main ways to connect a callback to an event.

#### 1. Connecting a standard function
You can pass a function reference directly.

```lua
local function LogDamage(amount, source)  
    print(string.format("Took %d damage from %s", amount, source))  
end  

OnPlayerDamaged:Connect(LogDamage)
```

#### 2. Connecting a class method with context (Recommended for OOP)
If you are using classes (as described in *Basic Concepts*), you usually want the callback to be a method of your class so it can access `self`. 

You can do this by passing the **function and the context table**, OR by passing the **method name as a string and the context table**.

```lua
local Player = {  
    health = 100,  
    
    -- Method that uses 'self'
    OnDamage = function(self, amount)  
        self.health = self.health - amount  
        print("Player health: " .. self.health)  
    end  
}  

-- Option A: Pass function and context table
OnPlayerDamaged:Connect(Player.OnDamage, Player)

-- Option B: Pass method name as string and context table (Cleaner!)
OnPlayerDamaged:Connect("OnDamage", Player)
```
> 💡 **Why pass the context table?** If you just connect `Player.OnDamage` without the context, `self` inside the function will be `nil`. Passing the table ensures `self` correctly points to your `Player` instance.

## Disconnecting from Events

When you no longer need to listen to an event (for example, when your object is destroyed), you **must** disconnect. Failing to do so will cause memory leaks and errors, as the event will try to call functions on destroyed objects.

To disconnect, use `:Disconnect()` and pass the **exact same arguments** you used when connecting.

```lua
-- Disconnecting
OnPlayerDamaged:Disconnect(LogDamage)
OnPlayerDamaged:Disconnect(Player.OnDamage)
```

> ⚠️ **Crucial Rule:** If you connected using an anonymous function, you must store its reference in a variable to disconnect it later!
> ```lua
> -- BAD: You can never disconnect this!
> OnPlayerDamaged:Connect(function(amount) print(amount) end)
> 
> -- GOOD: Store the reference
> local myHandler = function(amount) print(amount) end
> OnPlayerDamaged:Connect(myHandler)
> -- Later...
> OnPlayerDamaged:Disconnect(myHandler)
> ```