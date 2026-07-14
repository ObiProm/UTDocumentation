# TimedLabel

A custom `Label` that automatically hides itself after a specified duration. Useful for temporary messages, notifications, or floating combat text.

## Methods

### `TimedLabel:Show(text, time)`

Displays the label with the specified text for the given duration.

#### Parameters:
*   `text` (`string`) — The text to display.
*   `time` (`number`) — The duration in seconds before the label automatically hides.

#### Example:
```lua
timedLabel:Show("Level Up!", 2.5)
```

* * *

### `TimedLabel:Show(text, time, color)`

Displays the label with the specified text and color for the given duration. The label's color will automatically revert to its default color when it hides.

#### Parameters:
*   `text` (`string`) — The text to display.
*   `time` (`number`) — The duration in seconds before the label automatically hides.
*   `color` (`Color`) — The temporary color to apply to the label.

#### Example:
```lua
timedLabel:Show("Critical Hit!", 1.0, Color(1, 0, 0)) -- Red color
```

* * *