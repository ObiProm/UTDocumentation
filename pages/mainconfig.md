<h2>Main Config</h2>

<p>
You <b>must</b> create this configuration file – it's the foundation of your mod. Without it, the game simply won't recognize or load your mod at all.<br>
This file contains the essential information about your mod that players will see in the mod manager interface.
</p>

---

### Configuration File Structure

```json
{
    "Name": "Your mod",
    "Description": "Your interesting description",
    "Author": "Currens Ludos",
    "Version": "1.2.3.4",
    "Icon": "UTIcon.png"   
}
```

---

### Fields explained

- **Name**: The display name of your mod as it appears in the mod manager. Keep it short, memorable, and descriptive.  

- **Description**: A brief but informative description that helps players understand what your mod does. This appears below the mod name in the manager.  

- **Author**: Your name or username. This credits you as the creator and helps players identify your work.  

- **Version**: The current version of your mod using semantic versioning (major.minor.patch.build). This helps track updates and compatibility.  

- **Icon**: Filename of your mod's icon image. This appears as a visual identifier in the mod manager. 

---

### How It Appears in Game

<p>You will see something like this in the mod manager:</p>
<img src="images/ModManagerImage.png" alt="Mod manager interface showing the mod with icon, name, description, author, and version">

---

### Important Notes

1. **File Location**: This main configuration file must be placed in the root directory of your mod folder and should be named `config.json`.

2. **Not required Fields**: All fields shown in the example are not required

---

### Complete Example

```json
{
    "Name": "Epic Tower Wars",
    "Description": "Adds 3 new game modes, 5 custom maps, and 12 unique towers with special abilities.",
    "Author": "GameDevStudio",
    "Version": "2.1.0.5",
    "Icon": "Icons/ETW_Icon.png"
}
```

This configuration would display in the mod manager with your custom icon, mod name, full description, author credit, and version number – giving players all the information they need to decide whether to enable your mod.