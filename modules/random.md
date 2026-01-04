# random

Example Script:
```lua
--[[
--  @title
--      random_test.lua
--
--  @author
--      typedef
--
--  @description
--      testing randomness generator
--]]
local random_test = {}

function random_test.on_loaded( )

    -- random module
    local random = fantasy.random( )

    -- random array of numbers
    local arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 }

    -- generate random seeds to test true randomness.
    for i = 1, 5 do
        fantasy.print( "random int: {}", random:int( 1, 500 ) )
        fantasy.print( "random double: {}", random:double( 1.0, 500.0 ) )
        fantasy.print( "random float: {}", random:float( 1.0, 500.0 ) )
        fantasy.print( "random bool: {}", random:bool( ) )
        fantasy.print( "random string: {}", random:string( 5 ) )

        local rgb = random:rgb( )
        fantasy.print( "random rgb: {}, {}, {}", rgb[ 1 ], rgb[ 2 ], rgb[ 3 ] )

        local rgba = random:rgba( )
        fantasy.print( "random rgba: {}, {}, {}, {}", rgba[ 1 ], rgba[ 2 ], rgba[ 3 ], rgba[ 4 ] )

        -- pick a random element out of array
        fantasy.print( "random element: {}", random:element( arr ) )

        -- roll a chance (30%/100)
        local success, outcome = random:chance( 30 )
        fantasy.print( "30% chance: {} ({})", success, outcome )
    end

    -- display array and shuffle
    for i = 1, 5 do

        local output = ""
        for _, value in pairs( arr ) do
            output = output .. " " .. value
        end

        fantasy.print( "{}", output )
        random:shuffle( arr )
    end

end

return random_test
```

------------

## ```int```
###Type
`function`

###Parameters
- `number` min
- `number` max

###Returns
- `number` 

------------

## ```double```
###Type
`function`

###Parameters
- `number` min
- `number` max

###Returns
- `number`

------------

## ```float```
###Type
`function`

###Parameters
- `number` min
- `number` max

###Returns
- `number`

------------

## ```bool```
###Type
`function`

###Returns
- `boolean`

------------

## ```string```
###Type
`function`

###Parameters
- `number` length

###Returns
- `string`

------------

## ```rgb```
###Type
`function`

###Returns
- `number`
- `number`
- `number`

------------

## ```rgba```
###Type
`function`

###Returns
- `number`
- `number`
- `number`
- `number`

------------

## ```element```
###Type
`function`

### Description
Picks a random element inside a table.

###Parameters
- `table`

###Returns
- `any`

------------

## ```shuffle```
###Type
`function`

### Description
Shuffles a table. This overwrites the table passed. It does not return a temporary table.

###Parameters
- `table`

------------

## ```chance```
###Type
`function`

### Description
Determines a chance out of 100. If the number is lower than the submitted argument, the function will succeed.

###Parameters
- `number` 

###Returns
- `boolean` success
- `number` output

------------