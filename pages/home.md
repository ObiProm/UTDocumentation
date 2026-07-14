## Main Page

Welcome to **Uninfected Tower (UT)** documentation!

This page is an introduction, so you can understand what this documentation is about.

At the beginning, it's worth mentioning that **the game is built on the Godot engine** (using C# .NET), and all mechanics are directly related to this engine. **The modding language is Lua.** If you're unfamiliar with Lua, we recommend checking the [documentation](https://www.lua.org/docs.html). It would also be good to know the Godot base by reading their [documentation](https://docs.godotengine.org/en/stable/).


Since the game is based on Godot, we use Godot Nodes as the basic objects. The models are also stored as scenes, just like in Godot.

Our modified Lua is called **ULua**. The documentation will focus on ULua and creating addons, as well as how they work and the developer tool.

### Download game

Game is still in development, you can download alpha version of it download at **[google drive](https://drive.google.com/file/d/1GIUlthElBRDkEDTYf6zcMivwp2_lytUu/)**

Also visit our socials: [Discord](https://discord.gg/4a4e22Gqbu) and [Telegram](https://t.me/CurrensLudos)

## ULua API

### Main ideas

Every node, which was created by lua code is just table wrapper for Godot node class with specific metatable. It means that you can still use native functions (not all), and add custom fields for this node.
But sometimes nodes are not tables (we are trying to fix it, repot this bugs), like after using `PackedScene:Instantiate()`, so you need to create wrapper for it by `game.CreateNodeWrapper()`. 

### Using

We recomend to use **Visual Studio Code** with [sumneko lua extension](https://marketplace.visualstudio.com/items?itemName=sumneko.lua) and add our [addon](https://github.com/ObiProm/ULuaAddon)

### Supported file formats 
- Images: PNG, JPG, SVG, WebP, DDS 
- Audio: MP3 (WAV will be supported in future)

<br>

See [Node](pages/node.md).