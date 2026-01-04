# on_script_loaded

## Description
This callback is called when any script is loaded.

## Parameters
- `string` script_name

## Returns
- Returning `false` will prevent the script from being loaded.

## Example
```lua
function my_script.on_script_loaded( script_name )
    if script_name == "bad_script.lua" then
        return false
    end
end
```