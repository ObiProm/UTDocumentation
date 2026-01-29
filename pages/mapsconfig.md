## Maps Config

Create file `Maps.json` in your mod folder:

```json
{
    "Neon City": {
        "Icon": "icon16/city.png",
        "Description": "Forbidden city with neon lights and dark alleys.",
        "ScenePath": "Maps/NeonCity.tscn"
    }, 

    "Wild West": {
        "Icon": "Sprites/wild_west.png",
        "Description": "Dusty town in the wild west",
        "ScenePath": "Maps/Wild West.tscn"
    }
}
```

### Fields explained

- **Header** (like "Neon City") - The name players will see in map selection
- **Icon** - Path to icon image shown in menus  
- **Description** - Short text description of the map  
- **ScenePath** - Path to the actual map file (.tscn)  

All paths are relative to your mod folder.

You must add this file to your [main config](pages/mainconfig.md):

```json
{
    "MapsConfig": "Maps.json"
}
```