# WaveParser

Manages, parses, and executes enemy wave sequences. You can access the active instance of this manager via `game.GetWaveParser()`.

### How it Works
The `WaveParser` reads wave configurations (either from text resource files or manually added data) and asynchronously processes spawn commands over time. 

```waves
#comment example

# Wave reward
WaveReward 0
# Wave length (duration in seconds)
WaveLenght 40
# Time until the wave can be skipped
WaveSkipTime 5

# Wave spawn sequence starts here
WaveStart
	# <type> <count | optional, default = 1> <delay | optional, default = 1>
	Normal 4 1
	
	# Simple delay, accepts both whole and fractional numbers
	Wait 2.5
	
	Speedy 9 0.5
	Wait 10
	
	NormalBoss 1
WaveEnd
```

A standard wave configuration file follows this structure:
1. **Header Arguments** (Optional, before `WaveStart`): Key-value pairs defining wave properties. Supported keys:
   - `WaveReward` (int): Currency rewarded upon completion (default: `0`).
   - `WaveLenght` (int): Duration of the wave in seconds (default: `30`).
   - `WaveSkipTime` (int): Time allowed to skip the wave (default: `30`).
2. **`WaveStart`**: A mandatory marker indicating the beginning of spawn commands.
3. **Spawn Commands**: Executed sequentially. 
   - `Wait <seconds>`: Pauses execution for the specified time (e.g., `Wait 2.5`).
   - `<EnemyType> <Count> <Delay>`: Spawns a specific enemy type (**MUST BE CREATED AT ZOMBIES CONFIG**). `Count` is the number of enemies, and `Delay` is the time in seconds between each spawn (e.g., `Zombie 5 1.5` spawns 5 zombies with a 1.5-second delay between each).
4. **`WaveEnd`**: A mandatory marker indicating the end of the wave data.
5. **Comments**: Any line starting with `#` is ignored.

*Note: The parser handles spawning asynchronously, meaning it will not freeze the main thread while processing `Wait` commands or delayed spawns.*

---

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `CurrentWaveNumber` | `int` | The number of the currently active wave (read-only). |
| `TotalWaves` | `int` | The total number of loaded waves (read-only). |
| `AllEnemiesSpawned` | `bool` | Is enemies spawned at current wave (read-only). |
| `AsTable` | `Table` | MoonSharp Lua table representation of this parser instance (read-only). |

---

## Functions

### `WaveParser.StartWaves()`
Begins the wave sequence from the first wave. Resets the internal wave counter and triggers the first wave immediately.

---

### `WaveParser.AddWave(wave, fileKey)`
Manually loads and registers wave data from a string resource.

#### Parameters:
- `wave` (`int`) — The wave number to assign this data to.
- `fileKey` (`string`) — The key/identifier of the string resource containing the wave text data.

---

### `WaveParser.SetNextWaveTime(time)`
Manually overrides the timer for the next wave.

#### Parameters:
- `time` (`double`) — The time in seconds to wait before the next wave starts.

---

### `WaveParser.GetNextWaveTime()`
Returns the remaining time until the next wave begins.

#### Returns:
- `double` — Time left in seconds.

---

### `WaveParser.Stop()`
Halts the wave progression immediately. Stops the wave timer and awaits the completion of any currently active asynchronous spawning tasks before clearing them.

---

## Events

| Event | Parameters | Description |
|-------|------------|-------------|
| `OnWaveStarted` | `int waveNumber`, `WaveData waveData` | Emitted when a new wave begins. Provides the wave number and parsed data (reward, length, etc.). |
| `OnWavesEnded` | *None* | Emitted when all configured waves have been completed. |
| `OnEnemySpawnRequested` | `string enemyType` | Emitted for *each individual enemy* that needs to be spawned. Modders should listen to this event to actually instantiate the enemy entity in the game world. |

--- 