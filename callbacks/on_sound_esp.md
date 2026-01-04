# on_sound_esp

## Description
This callback is called whenever the Sound ESP is triggered from `constellation.lua`.

## Parameters
- `table`
      - `number` current_time
      - `number` next_allowed_time
      - `number` distance
      - `number` fov
      - `number` direction
      - `entity` entity
      - `vector` angle
      - `vector` bone

## Returns
- Returning `false` will prevent the Sound ESP from being played.

## Example
```lua
function my_script.on_sound_esp( data )
    -- completely disables sound esp regardless of `constellation.lua:esp` setting.
    return false
end
```