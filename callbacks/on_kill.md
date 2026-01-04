# on_kill

## Description
This callback is called when Omega assumes that the localplayer killed a target. This only works if Humanizer4 is enabled.

## Parameters
- `address` target

## Example
```lua
function death_callbacks.on_kill( address )

    -- to player
    local player = players.to_player( address )
    if not player then return end

    -- player name
    local name = player:get_name( )
    if not name then return end

    fantasy.print( "{} died", name )

end
```