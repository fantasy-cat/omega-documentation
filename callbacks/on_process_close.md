# on_process_close

## Description
This callback is called when the set process is closed.

## Parameters
- `string` name

## Example
```lua
function my_script.on_process_close( name )
    fantasy.log( "process closed: {}", name )
end
```