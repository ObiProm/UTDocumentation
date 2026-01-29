# First mod

To create mod you need to visit your game folder and go to the `mods` folder.

Create a folder with any name, the folder name won't affect anything.<br>
In order for the game to start reading the folder as a mod, it must contain a `config.json` file. So create it and open with any text editor.<br>
Read about this config [here](pages/mainconfig.md), but we will use incomplete configuration to simplify the task

```json
{
    "Name": "My mod name",
    "Description": "This is my first mod",
    "Author": "Cool guy",
    "Version": "0.0.0.1",
    "Icon": "CoolIcon.png"   
}
```

So put icon somewhere or delete this line (placeholder will be shown)

## First lua

We recomend to use Visual Studio Code with lua extension by sumneko: https://marketplace.visualstudio.com/items?itemName=sumneko.lua<br>
And also use our addon to syntax hylight: https://github.com/ObiProm/ULuaAddon

Lets write script, whic will print into console `Hello world!`

1. Create folder `lua/autorun` into your mod folder
2. Create lua file in `lua/autorun` with any name
3. Open it with any text editor
4. Write in file `print("Hello world!")`
5. Check it in game