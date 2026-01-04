# on_player_death

## Description
This callback is called when the localplayer dies.

## Parameters
- `address` localplayer

## Example
```lua
function death_callbacks.on_player_death( localplayer )

    if not localplayer then
        fantasy.print( "we disconnected? our localplayer doesn't exist anymore")
        return
    end

    fantasy.print( "we died! ({})", localplayer )

end
```