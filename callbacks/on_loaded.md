# on_loaded

## Description
This callback is called when a script is loaded.

## Parameters
- `table`
      - `string` name
      - `string` buffer
      - `boolean` toggled
      - `userdata` state
      - `number` id

## Returns
- Returning `false` will prevent the script from being loaded.

## Example
```lua
function my_script.on_loaded( data )
    fantasy.log( "my script's loaded (id: {})", data.id )
end
```