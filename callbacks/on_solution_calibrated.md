# on_solution_calibrated

## Description
This callback is called when `constellation.lua` is calibrated to CS2 or TF2.

## Parameters
- `table`
    - `string` name
    - `number` gameid

## Returns
- Returning `false` will prevent the script from being loaded.

## Example
```lua
function my_script.on_solution_calibrated( data )
    if info.gameid ~= GAME_CS2 then
        fantasy.log("This script only supports CS2. Exiting...")
        return false
    end
end
```