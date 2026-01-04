# on_humanizer_pre

## Description
This callback is called whenever the Humanizer is triggered from `constellation.lua`. This callback is called before the Humanizer is applied. `on_humanizer` is when the Humanizer is applying cursor movement.

## Parameters
- `table`
    - `number` ammo
    - `number` shots_fired
    - `entity` last_target
    - `entity` entity
    - `number` bone_id
    - `number` direction
    - `number` true_fov
    - `number` static_fov
    - `number` distance
    - `vector` angle
    - `vector` bone

## Returns
- Returning `false` will prevent the Humanizer from being activated.
- Returning a `number` will force a pulling value of the Humanizer and skip the smoothing algorithm.

## Example
```lua
function my_script.on_humanizer_pre( data )
    -- skip dynamic smoothing algorithm based on numerous factors to force 12 pulling value (not recommended).
    return 12
end
```