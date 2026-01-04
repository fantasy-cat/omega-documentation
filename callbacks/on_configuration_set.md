# on_configuration_set

## Description
This callback is called when any script uses `configuration:set`.

## Parameters
- `table` configuration

## Example
```lua
function my_script.on_configuration_set( config )
    fantasy.log( "configuration updated" )
    for key, value in pairs( config ) do
        fantasy.log( "key: {}, value: {}", key, value )
    end
end
```