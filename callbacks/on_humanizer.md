# on_humanizer

## Description
This callback is called whenever the Humanizer cursor movement is triggered from `constellation.lua`. This callback is only triggered when the Humanizer is successful in activation.

## Parameters
- `table`
    - `number` ammo
    - `number` shots_fired
    - `entity` last_target
    - `number` x
    - `number` y
    - `number` pull
    - `boolean` is_one_tapping
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

## Example
```lua
function my_script.on_humanizer( data )
    if data.is_one_tapping then
        fantasy.log( "disabled one-tapping module" )
        return false
    end
end
```