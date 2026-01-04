# scripts

## ```get_all```
###Type
`function`

###Description
Calls `getAllScripts` in the Web API and returns it as a nested table.

###Returns
- `table`

------------

## ```get_loaded```
###Type
`function`

###Description
Gets all currently loaded scripts as a nested table.

###Parameters
- `boolean` local_scripts_only

###Returns
- `table` script

------------

## ```reset```
###Type
`function`

### Parameters
- `boolean` include_local_scripts

###Description
Reloads all scripts. If the `boolean` parameter is `true`, this will also reload all local scripts, rather than only Cloud.

------------

## ```install_core```
###Type
`function`

###Description
This will install any core scripts in your `/scripts/core/` directory. FC2 already does this for you automatically once the Lua module is loaded. Therefore, if a script is already installed and loaded, it will not do it again. 

This function should only be used if you wish to install any core scripts that haven't been installed and loaded. A practical example would be a Lua script creating a file inside of `/scripts/core/`, and then calling this function to automatically install the core script without having the member restarting their solution.

------------

## ```is_loaded```
###Type
`function`

###Description
Wrapper for calling `scripts:get_loaded` and numerous comparison operations.

### Parameters
- `string`

### Returns
- `boolean`

------------

## ```reload```
###Type
`function`

###Description 
Allows you to reload a single script instead of constantly having to reload all scripts/restart solution.

### Parameters
- `string` script name

### Example
This example will make `on_loaded` get called twice.
```lua
local test = {}

function test.on_loaded( )
    fantasy.log("loaded")
end

function test.on_scripts_loaded( )

    -- reload self
    fantasy.scripts():reload( "test.lua" )
end

return test
```
------------

## ```load```
###Type
`function`

###Description
Loads a local file Lua script.

### Parameters
- `string` path

### Returns
- `boolean`

------------

## ```load_raw```
###Type
`function`

###Description
Loads a lua script based on script content.

### Parameters
- `string` name
- `string` content

### Returns
- `boolean`

------------

## ```get_stats```
###Type
`function`

###Description
Get the performance stats of scripts.

### Returns
- `table`

------------