## Mod structure

Mods have lua folder with `autorun`</code>` folder.
Scripts in this folder will start after all systems loaded, but before menu started to render.


<hr>

### Example structure:

```
YourCoolMod/
└── config.json
└── Gamemodes.json
└── Maps.json
└── Towers.json
└── lua/
    └── autorun/
        └── lua_script1.lua
        └── lua_script2.lua
└── ...
```