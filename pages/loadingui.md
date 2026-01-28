## LoadingUI

Controls the loading screen interface.

* * *

### `LoadingUI.SetPercentage(number)`

Sets the progress bar value.

#### Parameters:

*   `number` (`number`) — Progress value from 0 to 100.

#### Example:

LoadingUI.SetPercentage(75)

* * *

### `LoadingUI.SetStatus(text)`

Updates the status text on the loading screen.

#### Parameters:

*   `text` (`string`) — The status message.

#### Example:

LoadingUI.SetStatus("Loading assets...")

* * *

### Other

| LoadingUI.Show() | Displays the loading UI by playing the forward animation. |
| --- | --- |
| LoadingUI.Hide() | Hides the loading UI by playing the reverse animation. |