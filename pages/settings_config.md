## Settings config

```json
{
    "Audio": {
        "Towers": {
            "Priority": 1,
            "dj_volume":
            {
                "DefaultValue": 1,
                "Type": "Range",
                "Header": "DJ music volume",
                "ShowPercentage": true,
                "MinValue": 0,
                "MaxValue": 1,
                "Step": 0.01
            }
        }
    }
}
```

### Fields explained

- **Category name** - table of subcategories
  - **Prioryty** - shows how the category will be positioned close to the beginning (left side) of the settings list.
  - **Subcategory name**
    - **Prioryty** - shows how the subcategory will be positioned close to the top of the settings list.
    - **Table of setting**
      - **DefaultValue** - if the setting is not found in the saves, this value will be set.
      - **Other setting data...**

### Filling table of setting

Everything depends on **Type**, the rest of the settings simply set the values to the control that was created using the specified type.

Types:
 - InputBinding
 - Range
 - Check
 - Option

### Range

It is `LabeledSlider` node (Non godot node). So it has these fields:
 - Header
 - ShowPercentage - if off, shows setting value. If on, shows `{Value / (MaxValue - MinValue) * 100}%`, shows only 1 number after dot
 - MinValue - slider min value
 - MaxValue - slider max value
 - Value - slider current value
 - Step - slider step