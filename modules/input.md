# input

## ```is_key_down```
###Type
`function`

###Description
Checks if a key is down.

- Windows Key Codes: [https://cherrytree.at/misc/vk.htm](https://cherrytree.at/misc/vk.htm)

- Linux Key Codes: [https://www.cl.cam.ac.uk/~mgk25/ucs/keysymdef.h](https://www.cl.cam.ac.uk/~mgk25/ucs/keysymdef.h)

If you are on Linux, providing 1, 2, or 3 as an argument will let you check if your mouse buttons are down. The key codes on Linux do not register mouse input on every desktop environment. Therefore if you are trying to see if your left mouse button is down, you would provide `1`, `2` for right click and `3` for middle mouse button.

###Parameters
- `number`

###Returns
- `boolean`

------------

## ```click```
###Type
`function`

###Description
Simulates a mouse click.

###Parameters
- `number` button
    - 1: Left
    - 2: Right
    - 3: Middle

------------

## ```move```
###Type
`function`

###Description
Simulates mouse movement (relative).

###Parameters
- `number` x
- `number` y

------------

## ```move_raw```
###Type
`function`

###Description
Simulates mouse movement (relative) except this is done through low-level input, [allowing usage through raw input processes](https://constelia.ai/forums/index.php?threads/fc2.7854/post-67941).

###Parameters
- `number` x
- `number` y

------------

## ```get_mouse_position```
###Type
`function`

###Description
Gets mouse position.

###Returns
- `vector` position

------------

## ```key```
###Type
`function`

###Description
Presses a virtual key down for a certain amount of milliseconds.

###Parameters
- `number` virtual_key
- `number` sleep_ms

------------

## ```keyp```
###Type
`function`

###Description
Presses a virtual key down but the key is not released until `keyr` is called. This function is dangerous and should be used appropriately. If you do not call `keyr`, your system will constantly hold down the key regardless if the FC2 solution is closed or not. You will need to restart your system for the key to be released.

###Parameters
- `number` virtual_key

------------

## ```keyr```
###Type
`function`

###Description
Releases a key that is pressed down via `keyp`. If you call this function without `keyp`, your system might not react to that specific virtual key from being pressed down until you restart your system. Use this function with caution.

###Parameters
- `number` virtual_key

------------

## ```get_key_name```
###Type
`function`

###Description
Gets the formatted name of a key code.

###Parameters
- `number` virtual_key

###Returns
- `string`

------------

## ```clickp```
###Type
`function`

###Description
Holds down a mouse button. This should followed up with `clickr` at some point or else your mouse will forever be held down even if the program is closed.

###Parameters
- `number` button
  - 1: Left
  - 2: Right
  - 3: Middle

------------

## ```clickr```
###Type
`function`

###Description
Releases a held down mouse button. This function should only be used if you are completely certain the mouse key is down. `clickp` is the only instance of this being relevant. If you simply call this function even if the mouse key isn't down, your Windows will lock the mouse button until you restart your system.

###Parameters
- `number` button
  - 1: Left
  - 2: Right
  - 3: Middle

------------

## ```move_to_angles```
###Type
`function`

###Description
This will automatically convert a destination angle position to pixels and then move your cursor for you. This function works well with the `entity_list:get_closest` function which returns `angle`.

The `mouse threshold` parameter is optional and works like `humanizer_mouse_threshold` in Constellation4.

The `arc_bend` parameter is optional and automatically applies arc/bending-like behavior to the algorithm. This setting is tweaked via `os.lua:move_to_angles_arc_bend_strength` and `os.lua:move_to_angles_arc_bend_speed`. GIF below as an example:

![](https://i.imgur.com/82I5EdV.gif)

###Parameters
- `vector` destination
- `number` smoothness
- `number` mouse threshold (optional)
- `boolean` arc_bend (optional)

### Returns
- `number` x
- `number` y

------------

## ```move_to_angles_raw```
###Type
`function`

###Description
Same as `move_to_angles`. At one point, this function was needed for raw input situations. The function is defunct.

------------

## ```is_window_focused```
###Type
`function`

###Description
Checks if your input is currently focused on a window. 

This function varies depending on your OS. On Windows, you can check if a window is focused based on the class or the title of the window. On Linux, only the window class is acceptable. You can use `xprop` on Linux to see a window class (`WM_CLASS`). The reason why Linux's version of this function works differently is because certain WMs may modify or "flavor" the title of a window, thereby creating inconsistencies. See example.

You should never provide both parameters with an argument. Only one should be provided at a time. If you provide both, `class` will automatically be assumed fulfilled, and `title` will be ignored.

Even if you are a Windows user, you should always be considerate towards the Linux community at constelia.ai. See the example below to provide compatibility for both platforms.

###Parameters
- `string` class
- `string` title

### Example
```lua
local test = {}

function test.on_worker() 

    -- input module (or just use lib_modules:input since it's faster)
    local input = fantasy.input( )

    -- display if window focused
    if fantasy.os == "linux" then
        fantasy.log( "is_focused: {}", input:is_window_focused( "cs2", "" ) )
    else
        fantasy.log( "is_focused: {}", input:is_window_focused( "", "Counter-Strike 2" ) )
    end

end

return test
```

------------