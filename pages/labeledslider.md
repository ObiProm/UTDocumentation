# LabeledSlider

A custom UI control that combines a header label, a value display, and a horizontal slider (`HSlider`). Designed for exposing adjustable numeric parameters in the game UI.

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `Header` | `string` | The text displayed as the header of the slider. Default: `"Parameter"`. |
| `ShowPercentage` | `boolean` | If `true`, displays the value as a percentage (0–100%) relative to `MinValue` and `MaxValue`. Default: `false`. |
| `MaxValue` | `number` | The maximum allowed value of the slider. Default: `100`. |
| `MinValue` | `number` | The minimum allowed value of the slider. Default: `0`. |
| `Step` | `number` | The increment step of the slider. Default: `1`. |
| `Value` | `number` | The current value of the slider. Automatically clamped between `MinValue` and `MaxValue` and rounded to 2 decimal places. Default: `50`. |

### Events

<div class="markdownTable">

| Event | Parameters | Description |
|-------|------------|-------------|
| `OnValueChanged` | `value` (`number`) | Invoked when the slider value changes, either by user interaction or by setting the `Value` property via code. |

</div>