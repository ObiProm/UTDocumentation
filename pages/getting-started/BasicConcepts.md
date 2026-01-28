# Basic api

Lets start with some code! You have to understand that the whole structure of modding is tied to creating classes, they work like godot nodes. Basically, it's the same as if you decided to write a game for Godot, as well as create a separate class for the node, etc.

So let's see base API, which you will use later

```lua
local node = game.CreateNode("Node3D")
node.Position = Vector3(1, 1, 1)
game.GetCurrentScene().AddChild(node)
```

This code creates node and adds to current scene and sets node's position to (1, 1, 1). In `game.CreateNode(className)` you can create any godot node.

> 💡 **Important distinction:** `game.CreateNode()` creates objects that live **inside the scene tree** (they have `_Ready`, `_Process`, can be added as children). If you need a "pure" Lua object for storing data, resources, or managers that don't need to exist in the scene tree, use `game.CreateUserData()` instead. UserData is lighter and doesn't participate in Godot's node lifecycle. You can use it for godot types (Resources) like `AudioStream` etc.

# Inheritance

Let's see how to create your own class. You need to use `game.RegisterClass(className, table, baseType?)`, baseType is optional, default is `Node`.

```lua
local superNode = {}

function superNode:Talk(message)
    print("Super node said:", message)
end

game.RegisterClass("SuperNode", superNode)

--- Calling it
local super = game.CreateNode("SuperNode")
super:Talk("Hi!") -- Super node said: Hi!
```

You can also inherit your own classes from other classes (including game classes). To access the parent class's table, use `self.BaseClass` (it will be `nil` if the base type is raw userdata like `Node3D`).

```lua
local superNodev2 = {}

-- Rewriting SuperNode's function
function superNodev2:Talk(message)
    print("I'm super node ver2, and I said:", message)
end

game.RegisterClass("SuperNodev2", superNodev2, "SuperNode")

--- Calling it
local super = game.CreateNode("SuperNodev2")
super:Talk("Hello") -- I'm super node ver2, and I said: Hello
super.BaseClass:Talk("Hello") -- Super node said: Hi!
```

# Virtual functions

Virtual functions are special methods that the engine/game calls automatically at specific moments. You often just define them, and the engine/game will trigger them when needed. But you also can call it.

Every node has these basic virtual functions:

| Function | When called | Use case |
|----------|-------------|----------|
| `_Init` | Right after `game.CreateNode()` | Initialize something, like constructor in C languages |
| `_Ready` | When node enters the scene tree | Access children, set up UI, connect signals |
| `_Process` | Every frame | Movement, timers, input handling |

Lets see on example
```lua
local MyNode = {}

-- Called right after game.CreateNode()
function MyNode:_Init()
    print("I was called before `_Ready!`")
end

-- Called when node enters the scene tree (after AddChild)
function MyNode:_Ready()
    print("I'm in the scene now!")
    local child = self:GetChild(0)
end

-- Called every frame while node is in the scene
function MyNode:_Process(delta)
    print("Frame tick: " .. delta)
end

game.RegisterClass("MyNode", MyNode)
```

Some types like `Tower` has their own virtual functions, and we learn it later