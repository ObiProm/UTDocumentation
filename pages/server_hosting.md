## Core Systems

### Server Hosting

Dedicated servers can be configured through a JSON file and command-line arguments. If server started, host player can open panel with all players to kick/ban them by IP. Also can unban in another menu.

#### Configuration File
Server settings are stored in `user://ServerConfig.json`. This file is auto-generated with default values on first launch:

```json
{
  "Name": "My server",
  "ShortDescription": "",
  "Description": "",
  "Icon": "ServerIcon.png",
  "MaxPlayers": 128,
  "PublicPort": 4343,
  "PrivatePort": 1111
}
```

#### Key Parameters

<div class="markdownTable">

| Parameter | Description |
|-----------|-------------|
| `Name` | Public server name shown in server browsers |
| `ShortDescription` | Brief description for server listings |
| `Description` | Detailed server description |
| `Icon` | Path to server icon image (loaded from mod forder) |
| `MaxPlayers` | Maximum player capacity |
| `PublicPort` | Port for server browser queries (informational) |
| `PrivatePort` | Port for actual gameplay connections |

</div>

#### Command-Line Arguments
Start the server using the `--server` flag. Override any setting with `--<parameter>=<value>`:

```bash
"Uninfected Tower.exe" --server --name="Community Server" --maxplayers=32
```

- All parameters are case-insensitive (`--NAME` = `--name`)
- Command-line values override and persist to `ServerConfig.json`
- Invalid values (e.g., text for numeric ports) are rejected with warnings

#### Port Behavior
- **PublicPort**: Used exclusively by server browsers to fetch metadata (player count, description, etc.)
- **PrivatePort**: Handles all game traffic and client connections
- Both ports must be open in your firewall for proper operation

#### Startup Process
1. Server launched with `--server` flag
2. Loads `ServerConfig.json` (creates default if missing)
3. Applies command-line overrides
4. Saves updated configuration
5. Binds to specified ports and starts accepting connections

Successful startup logs:
```txt
Started server 'Community Server' at 4343 with max players 32
```

#### Practical Example
Create mod with icon at `Sprites/custom_icon.png` (example path)<br>
Configure `ServerConfig.json`:
```json
{
  "Name": "Modded Fun Server",
  "Icon": "Sprites/custom_icon.png",
  "MaxPlayers": 24
}
```
Launch server:
```bash
"Uninfected Tower.exe" --server --publicport=8888 --privateport=7777
```