# script

## ```id```
###Type
`number`

------------

## ```name```
###Type
`string`

------------

## ```toggled```
###Type
`boolean`

------------

## ```state```
###Type
`userdata`

### Description
This is the `lua_State` associated with the script.

------------

## ```callbacks```
###Type
`table`

### Description
This will list all the functions considered callbacks in FC2 that the script uses. The keys contain the names of the callback, and the value contains the Lua reference.

### Example
```lua
local lua_state = {}

function lua_state.on_loaded( )

    ---@diagnostic disable-next-line: undefined-global
    fantasy.print( "lua_state: {}", _FANTASYSDKSCRIPTSTATE_ )

end

function lua_state.on_scripts_loaded( )

    for _, v in pairs( fantasy.scripts():get_loaded( true ) ) do

        fantasy.print("{}: {}",
            v.name,
            v.state
        )

        for callback, ref in pairs( v.callbacks ) do
            fantasy.print("     -> {}: {}",
                callback,
                ref
            )
        end

    end

end

return lua_state
```

------------


## ```buffer```
###Type
`string`

------------

## ```cloud```
###Type
`boolean`

------------

## ```disable```
###Type
`function`

------------

## ```enable```
###Type
`function`

------------