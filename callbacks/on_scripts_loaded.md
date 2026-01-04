# on_scripts_loaded

## Description
This callback is triggered when all scripts are loaded. 

This callback is the most reliable way to manage scripts. For example, if you are trying to unload a script through `on_script_loaded`, your script may be loaded **after** that callback is triggered. Therefore, you will miss the timing. By using the `scripts` module in this callback, you can safely unload or manage other actively running scripts.

## Example
```lua
function my_script.on_scripts_loaded( )
    fantasy.log( "all scripts are loaded now" )
end
```