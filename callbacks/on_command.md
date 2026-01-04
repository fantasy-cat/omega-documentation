# on_command

## Description
This callback is called when any input is submitted through the terminal/console.

## Parameters
- `string` text

## Example
```lua
function my_script.on_command( text )
    fantasy.log( "{} was typed into console/terminal", text )
end
```