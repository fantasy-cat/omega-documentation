# entity

## ```read```
### Type
`function`

### Description
See `address:read`.

------------

## ```get_pawn```
### Type
`function`

### Description
Gets the pawn of this entity. CS2 only.

### Returns
- `address`

------------

## ```get_index```
### Type
`function`

### Description
Gets the index of this entity.

### Returns
- `number`

------------

## ```is_dormant```
### Type
`function`

### Description
Checks if this entity is dormant.

### Returns
- `boolean`

------------

## ```get_box_dimensions```
### Type
`function`

### Description
Gets the dimensions of this entity's box.

### Returns
- `table`
    - `number` left
    - `number` top
    - `number` right
    - `number` bottom
    - `vector` origin
    - `vector` head
    - `vector` screen_head
    - `vector` screen_origin

------------

## ```get_class```
### Type
`function`

### Description
Gets the class of this entity.

### Returns
- `number` class_id
- `string` class_name

------------

## ```get_bone```
### Type
`function`

### Description
Gets the position of a bone.

### Parameters
- `number` bone_id

### Returns
- `vector` bone_position
- `number` fov
- `vector` angle
- `number` scaled_fov

------------

## ```get_closest_bone```
###Type
`function`

### Description
Finds the nearest bone within a set of bone IDs provided.

### Parameters
- `table` bones

### Returns
- `number` bone_id
- `number` fov
- `vector` bone_position
- `vector` angle

### Example
```lua
local modules = require( "modules" ) -- lib_modules
local players = require( "players" ) -- lib_players
local bone_example =
{
    fov = 2
}

--- on_worker
--- @param is_calibrated any
function bone_example.on_worker( is_calibrated )

    -- not calibrated
    if not is_calibrated then return end

    -- get localplayer (convert to lib_players)
    local localplayer = players.to_player( modules.entity_list:get_localplayer( ) )
    if not localplayer then return end

    -- get closest entity (convert to lib_players)
    local enemy = players.to_player( modules.entity_list:get_closest( ) )
    if not enemy then return end

    -- is spotted/visible?
    if not localplayer:is_spotted( enemy ) then return end

    -- get specific bone and its fov
    local closest_bone, fov, bone_position = enemy:get_closest_bone( { 3, 5, 7, 10 } )

    -- not in our fov
    if fov > bone_example.fov then return end

    -- in our fov, display the exact number
    print("in fov ({}/{}) with bone {} (@{})", fov, bone_example.fov, closest_bone, bone_position )
end

return bone_example
```

------------