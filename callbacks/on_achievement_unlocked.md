# on_achievement_unlocked

## Description
This callback is called when an achievement is unlocked.

## Parameters
- `string` name

## Example
```lua
function my_script.on_achievement_unlocked( name )
    fantasy.log( "achievement unlocked: {}", name )
end
```