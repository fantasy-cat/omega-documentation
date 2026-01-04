# engine:entity_list

## ```bones```
###Type
`function`

### Description
This will set which bones you want Constellation4 to scan in the worker. If you do not provide an argument, this function will return the bones in a `table`. If you do provide an argument, then you must provide a table of bones. See example.

### Parameters
- *`table` bones*

### Returns
- *`table` bones*

### Example
```lua
-- get entity list module
local entity_list = fantasy.engine.entity_list()

-- list all bones Constellation4 scans
for _, bone in pairs( entity_list:bones() ) do 
    print( bone )
end

-- set our bones 
entity_list:bones( { 3, 4, 7, 10 } )
```

------------

## ```fov```
###Type
`function`

### Description
This will set the FOV of Constellation4 when scanning for entities. If you do not provide an argument, this function will return the FOV. If you do provide an argument, then you must provide a `number`. See example.

### Parameters
- *`number` fov*

### Returns
- *`number` fov*

### Example
```lua
-- get entity list module
local entity_list = fantasy.engine.entity_list()

-- print our fov
print( entity_list:fov( ) )

-- set our fov
entity_list:fov( 8.2 )
```

------------

## ```friendly_fire```
###Type
`function`

### Description
This will determine the entity list worker in Constellation4 to consider friendly fire. If you do not provide an argument, this function will return the status of friendly fire. If you do provide an argument, then you must provide a `boolean`.

### Parameters
- *`boolean` status*

### Returns
- *`boolean` status*

------------

## ```get_localplayer```
###Type
`function`

### Returns
- `entity`

------------

## ```get_players```
###Type
`function`

### Returns
- `table`

------------

## ```get_teammates```
###Type
`function`

### Returns
- `table`

------------

## ```get_enemies```
###Type
`function`

### Returns
- `table`

------------

## ```get_in_fov```
###Type
`function`

###Description
This function not only returns a nested table of `entity`, but a few more values for each entity:


- `number` boneid
- `number` direction
- `vector` bone
- `vector` angle
- `number` distance
- `number` true_fov
- `number` static_fov

### Returns
- `table`

------------

## ```get_closest```
###Type
`function`

###Description
This function not only returns a `entity`, but a few more values for the entity:


- `number` boneid
- `number` direction
- `vector` bone
- `vector` angle
- `number` distance
- `number` true_fov
- `number` static_fov


### Returns
- `table`

------------

## ```get_entity```
###Type
`function`

###Parameters
- `userdata/number` entity handle or entity index

### Returns
- `entity`

------------

## ```get_viewangles```
###Type
`function`

### Returns
- `vector`

------------

## ```get_highest_entity_index```
###Type
`function`

### Returns
- `number`

------------

## ```get_max_entities```
###Type
`function`

### Returns
- `number`

------------

## ```get_entities```
###Type
`function`

### Description
This function returns a table of all entities in the game and also passes a `class` string. If you're only looking for players, use `get_players` instead.

### Returns
- `table`

------------

## ```from_handle```
###Type
`function`

### Parameters
- `number/address` handle

### Returns
- `entity`

------------

## ```get_player_resources```
###Type
`function`

### Returns
- `address`

------------

## ```get_localteam```
###Type
`function`

### Returns
- `number`

------------

## ```get```
###Type
`function`

### Description
Only works for games that aren't fully-fledged in the FC2 entity_list sub-module. This will get the pointer memory address of the entity list.

### Returns
- `address`

------------

## ```catfish_ray```
###Type
`function`

### Description
[See guide](https://constelia.ai/forums/index.php?threads/catfish-ray-behavioral-analysis-for-aimbot-related-visibility-detection-secure-your-aiming-scripts.11494/).

### Returns
- `number`

### Example
```lua
local modules = require( "modules" ) -- lib_modules 
local catfish_test = { }

function catfish_test.on_worker( is_calibrated )

    -- not calibrated
    if not is_calibrated then return end

    -- get closest
    local closest = modules.entity_list:get_closest( )
    if not closest then return end

    -- probability they are visible
    local probability = closest:catfish_ray( )

    -- assume if >X probability, we're going to ASSUME visibility
    -- we're going to assume they COULD be visible in an aimbot/legitbot situation
    -- we can also assume that in this situation, the localplayer (us) is actively in combat
    local threshold = 50

    -- display output. green if >threshold. red otherwise.
    modules.kernel:text(
        fantasy.fmt("visibility probability: {}%", probability ),
        24,
        150,
        250,
        probability < threshold and color:new( 255, 0, 0, 255 ) or color:new( 0, 255, 0, 255 )
    )

end

return catfish_test
```

------------