# engine.kernel

## ```is_fc2k_loaded```
###Type
`function`

###Returns
- `boolean`

------------

## ```is_parallax_loaded```
###Type
`function`

###Returns
- `boolean`

------------

## ```is_drawing```
###Type
`function`

###Description
Returns `true` if the member is using FC2K to render visuals instead of an overlay. This will always return `true` if the user is on Linux or using the overlay module instead of FC2KV.

###Returns
- `boolean`

------------

## ```line```
###Type
`function`

###Parameters
- `number` x
- `number` y
- `number` x2
- `number` y2
- `number` thickness
- `color` color

------------

## ```box```
###Type
`function`

###Parameters
- `number` x
- `number` y
- `number` x2
- `number` y2
- `number` thickness
- `color` color

------------

## ```boxf```
###Type
`function`

###Description
Keep in mind that opacity is not considered when using FC2KV. Therefore, drawing a filled box will never include any sort of transparency.

###Parameters
- `number` x
- `number` y
- `number` x2
- `number` y2
- `color` color

------------

## ```text```
###Type
`function`

### Description
This will draw text on your screen using the FC2KV. See [the restrictions with this feature here (click me)](https://constelia.ai/forums/index.php?threads/fc2k-visuals-guide.8992/#post-70183). This function is very limited and shares the same roadblocks as other kernel drawing functions. Use appropriately.

###Parameters
- `string` text
- `number` font_size
- `number` x
- `number` y
- `color` color (optional)
- `number` font_id (optional)

### Example
```lua
local kernel = fantasy.engine.kernel()

-- draw text
kernel:text( 
    "Hello World. This is a test!", -- text
    18,                             -- font size
    250,                            -- x
    250                             -- y
)
```

### Example (Custom Font)
![](https://i.imgur.com/SQq5U7D.png)

------------

## ```circle```
###Type
`function`

###Description
There is an undocumented `circlef` function with the same parameters that will draw a filled circle. However, due to the limitations of FC2KV, the function will not work in FC2KV. It might work with the `overlay` module. Be careful when invoking this function as it pushes the limits of FC2KV.

###Parameters
- `number` x
- `number` y
- `number` radius
- `color` color

------------

## ```triangle```
###Type
`function`

###Description
There is an undocumented `trianglef` function with the same parameters that will draw a filled triangle. However, due to the limitations of FC2KV, the function will not work in FC2KV. It might work with the `overlay` module. Be careful when invoking this function as it pushes the limits of FC2KV.

###Parameters
- `number` x
- `number` y
- `number` x2
- `number` y2
- `number` x3
- `number` y3
- `color` color

------------

## ```draw```
###Type
`function`

###Description
Allows you to send custom drawing requests to FC2T. See example.

###Parameters
- `number` type ([FC2_TEAM_DRAW_TYPE](https://github.com/fantasy-cat/FC2T/blob/main/fc2.hpp#L184) value or custom number)
- `number` x (or left)
- `number` y (or top)
- `number` x2 (or right)
- `number` y2 (or bottom)
- `number` thickness
- `color` color

### Example
```lua
local custom_draw = {}
local kernel = fantasy.engine.kernel( )

function custom_draw.on_worker( )

    kernel:draw(
        7,      -- this is not an FC2_TEAM_DRAW_TYPE. 6 is CIRCLE_FILLED, 7 is nothing (can be used for custom)
        100,    -- x (or left)
        100,    -- y (or top)
        250,    -- x2 (or right)
        250,    -- y2 (or bottom)
        1,      -- thickness (if applicable - provide anyway)
        color:new( 255, 0, 0, 255 )
    )

end

return custom_draw
```

------------

## ```start_fc2kv```
###Type
`function`

###Description
This will start FC2KV in FC2K. 

This function will always fail if FC2KV is already running. By default, having `fc2.lua:kernel_drawing` on enables FC2KV when the FC2 solution is loaded. This function is only for scripts or projects that want to start FC2KV without `fc2.lua:kernel_drawing` being on.

###Returns
- `boolean`

------------

## ```exit_fc2kv```
###Type
`function`

###Description
This will unload FC2KV in FC2K.

This function will always fail if FC2KV is not running. If `fc2.lua:kernel_drawing` was off when the solution is started, this function always fail. Otherwise, it should naturally succeed.

###Returns
- `boolean`

------------

## ```update_aurora```
### Type
`function`

### Description
Same as `aurora.update`.

------------

## ```is_aurora_loaded```
### Type
`function`

### Description
Same as `aurora.is_loaded`.

------------

## ```load```
###Type
`function`

###Description
Loads an officially supported driver (`parallax`, `fc2k`, `aurora`).

###Parameter
- `string`

###Returns
- `boolean`

------------

## ```update_parallax```
###Type
`function`

###Description
Updates the latest configuration and sends it to the Parallax driver.

------------

## ```is_parallax_loaded```
###Type
`function`

###Description
Checks if Parallax2 is loaded.

###Returns
- `boolean`

------------

## ```image```
###Type
`function`

### Description
See [Images](https://constelia.ai/forums/index.php?threads/images.11487/#post-95113) guide.

###Parameters
- `number` x
- `number` y
- `number` width
- `number` height
- `userdata` texture

------------