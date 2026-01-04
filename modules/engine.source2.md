# engine.source2

## ```get_schema```
###Type
`function`

###Parameters
- `string` class
- `string` field

###Returns
- `number`

------------

## ```dump_schemas```
###Type
`function`

###Parameters
- `string` path

------------

## ```to_controller```
###Type
`function`

###Description
Gets the controller of a pawn.

###Parameters
- `entity/userdata`

###Returns
- `entity`

------------

## ```get_globals```
###Type
`function`

###Returns
- `table`
    - `address` address
    - `number` tick_count
    - `number` interval_per_tick
    - `number` interpolation_amount
    - `number` frame_count
    - `number` real_time
    - `number` cur_time
    - `number` frame_time
    - `number` max_clients
    - `string` map
    - `string` map_directory

### Example
```lua
local modules = require( "modules" ) -- lib_modules
local map = {}

function map.on_worker( is_calibrated )

	-- not calibrated 
	if not is_calibrated then return end

	-- get globals
	local globals = modules.source2:get_globals( )
	if not globals then return end

	-- output
	print( fantasy.fmt("globals: {}", globals.address ) ) -- show globals address just for debug
	print( fantasy.fmt("map: {} ({})", globals.map, globals.map_directory ) ) -- map (directory)

	-- get map name using globals.address in case of update or other required values not automatically added to the table (https://constelia.ai/forums/index.php?threads/map_name-and-map_directory-globals.10080/)
	local pdir = globals.address:read( MEM_ADDRESS, 0x1B0 )
	local pmap = globals.address:read( MEM_ADDRESS, 0x1B8 )
	local directory = pdir:read( MEM_STRING, 0, 32 )
	local name = pmap:read( MEM_STRING, 0, 32 )
	print( fantasy.fmt("manually: {} ({})", name, directory ) )
end

return map
```

------------