## Gamemodes Config

To use it, you must create file with any name, but you must add it to your mod's main config.  
See also [main config](#mainconfig)

```json
{
    "Standard": {
        "Description": "Standard mode with a variety of modifiers",
        "LoadingManagerScript": "StandardLoadingManager",
        "Modifiers": {
            "SplitRewards": {
                "Type": "bool",
                "Name": "Split Rewards",
                "Description": "Some description here"
            }
        },
        "AvailableMaps": [],
        "DisabledMaps": []
    }
}
```

### Fields explained

- **Description** - Short description of the gamemode shown to players
- **LoadingManagerScript** - Name of the lua class that runs when game starts with this mode  
  See also [Loading Manager](#loadingmanager)
- **Modifiers** - Custom settings players can configure for this game mode:
  - **Type** - Data type (`bool`, `number`, `string`)
  - **Name** - Display name shown to players  
  - **Description** - Explanation of what this modifier does
- **AvailableMaps** - List of map names that will be available for this mode  
  If not empty, only these maps will be available
- **DisabledMaps** - List of map names that will be hidden for this mode  
  If not empty, all maps except these will be available  


**Note**: If both `AvailableMaps` and `DisabledMaps` are empty or not stated, all maps are available.  

Add your gamemodes file to [main config](#mainconfig):

```json
{
    "GamemodesConfig": "Gamemodes.json"
}
```