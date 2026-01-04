# on_constelia_speak

## Description
This callback is called when Constelia verbally plays audio.

## Parameters
- `string` voiceline

## Returns
- Returning `false` will prevent her from playing her the voice line.

## Example
```lua
function my_script.on_constelia_speak( line )
    if line == "greeting" then
        return false
    end
end
```