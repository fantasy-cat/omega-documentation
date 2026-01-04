# on_configuration_overwrite

## Description
This callback is called when any script uses `configuration:overwrite`.

## Parameters
- `table` scripts_names

## Example
```lua
function my_script.on_configuration_overwrite( scripts )
    fantasy.log( "configuration was overwritten" )
end
```