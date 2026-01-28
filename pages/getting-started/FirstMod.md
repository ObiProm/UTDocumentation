# First mod

To create mod you need to visit your game folder and go to the `mods` folder.

1. Create a new folder with any name (e.g., `MyAwesomeMod`). The folder name does not affect anything in-game.
2. Inside that folder, create a file called `config.json` and open it in any text editor.

> 📖 For the full configuration reference, see [Main Config](pages/mainconfig.md).

Let's look at typical config

```json
{
    "Name": "My mod name",
    "Description": "This is my first mod",
    "Author": "Cool guy",
    "Version": "0.0.0.1",
    "Icon": "CoolIcon.png"   
}
```

Place an icon image (`CoolIcon.png`) in your mod folder, or simply delete the `"Icon"` line — a placeholder will be shown instead.

## Before You Code: Where Does `print()` Show Up?

Throughout this guide you will use `print()` to verify that your code runs. **You won't see it in the game window itself.** Look here instead:

| Where | How to open |
|:------|:------------|
| **In-game Developer Console** | Press <code>~</code> (tilde) or <code>F12</code> during gameplay (check your keybinds) |
| **Log file on disk** | Windows: `%appdata%/Uninfected Tower/logs/` · Linux: `~/.local/share/Uninfected Tower/logs/` |

---

## Folder structure

To make the game recognize your mod and properly load your custom content, your mod folder must follow this exact structure. The game's internal systems expect your files to be in specific locations.

```
MyAwesomeMod/
├── config.json             # Main mod config. Must be in the root folder.
├── lua/                    # Contains your Lua scripts.
│   └── autorun/            # Scripts placed here run automatically on game start.
└── Configs/                # Central folder for all game configurations.
    ├── Towers/             # Tower configs (e.g., archer.json)
    ├── Zombies/            # Zombie configs (e.g., walker.json)
    ├── Settings/           # Mod settings configs
    ├── Maps/               # Map configs
    └── Gamemodes/          # Gamemode configs
```

1. **`config.json`**: The entry point of your mod. The game will completely ignore your mod folder if this file is missing from the root.
2. **`lua/autorun/`**: This specific path is required. The game automatically scans this folder and executes any `.lua` file placed inside it on startup.
3. **`Configs/` and its subfolders**: This is **not optional**. The game automatically loads configuration files strictly inside these specific subfolders (`Configs/Towers/`, `Configs/Zombies/`, `Configs/Settings/`, `Configs/Maps/`, `Configs/Gamemodes/`). If you place your JSON files anywhere else, the game will not load them.

## First lua

We recomend to use Visual Studio Code with lua extension by sumneko: https://marketplace.visualstudio.com/items?itemName=sumneko.lua<br>
And also use our addon to syntax hylight: https://github.com/ObiProm/ULuaAddon

Lets write script, whic will print into console `Hello world!`

1. Create folder `lua/autorun` into your mod folder
2. Create lua file in `lua/autorun` with any name
3. Open it with any text editor
4. Write in file `print("Hello world!")`
5. Check it in developer console!
