# on_worker

## Description
This callback is called when Omega ticks or performs a CPU cycle. 

This callback should be the main way to interact with Omega and perform game hacking operations. You should not perform any game hacking operations outside this callback, excluding Humanizer-related callbacks. This is the most important callback in Omega. 

The callback's speed is directly related to the FPS system in `system.lua:worker_fps`. This is essentially the main background worker of Omega. Most scripts use `on_worker` to execute code. By default, this will run at 60 frames per second. Increasing this value will increase your CPU usage, and make the process become more resource hungry. It can also create instability in game hacking features.

## Parameters
- `boolean` calibrated_flag
- `number` game_id

## Example
```lua
function my_script.on_worker( is_calibrated, game_id )
    if not is_calibrated then
        fantasy.log( "omega is not calibrated. cannot utilize game hacking features" )
        return
    end
    
    fantasy.log( "omega is calibrated. game id: {}", game_id )
end
```