# fantasy (functions)

## ```log```
###Type
`function`

###Description
This accepts the [format string syntax](https://fmt.dev/11.0/syntax/#format-examples), which is similar to Python's [str.format](https://docs.python.org/3/library/stdtypes.html#str.format).

You can pass a class as an argument and it will automatically get the value. Passing the `color` class will output the RGBA and hex value for example. This should also work with `entity`, `vector` and `address`. This also applies to `fantasy.fmt`.

###Parameters
- `string` text

###Example
```lua
-- testing fmt and fantasy.log
local fmt = {}

function fmt.on_loaded( _, session )

    -- a simple and basic log entry and output to console
    fantasy.log( "Basic string" )

    -- a formatted log entry and output to console with index specification (optional)
    fantasy.log( "Hello! My name is {0} with {1} forum posts.", session["username"], session["posts"] )

    -- testing types
    local random_address = address.new( 0xDEADBEEF )
    local random_table = { 1, 2, 3, 4, 5 }
    local random_boolean = true
    fantasy.log( "{}", random_table )
    fantasy.log( "{}", random_address.address )
    fantasy.log( "{}", random_boolean )
    fantasy.log( "{:.2f}", 12.345678 ) -- this should round in console to 12.35
    fantasy.log( "{}", fmt.on_loaded )

    -- format and assign to a string with no index specification
    local welcome_message = fantasy.fmt( "Welcome {} to fantasy.{}", session["username"], string.lower( fantasy.solution ) )

    -- create notification using fantasy.fmt;
    fantasy.notification( "fmt-test", welcome_message )

    -- this should throw an exception instead of simply crashing your FC2 solution
    fantasy.log( "Hello! {} {} {} {} {}", 1000) -- this will throw an exception because you requested 5 specifiers but only included 1.

end

return fmt
```

------------

## ```fmt```
###Type
`function`

###Description
This accepts the [format string syntax](https://fmt.dev/11.0/syntax/#format-examples), which is similar to Python's [str.format](https://docs.python.org/3/library/stdtypes.html#str.format). See `log` function above for an example.

###Parameters
- `string`

###Returns
- `string`

------------

## ```print```
###Type
`function`

###Description
This is a wrapper for `fantasy.fmt` and `print`, which automatically prints the output to console only. This is essentially `fantasy.log`, except it only prints to console.

###Parameters
- `string`

###Example
```lua
local print_test = {}

function print_test.on_loaded( )

    -- string and number output
    fantasy.print( "Hello {}", "World" )
    fantasy.print( "My favorite number is {}", 1337 )

    -- vector class output
    local vec3 = vector:new( 10, 20, 30 )
    fantasy.print( "vec3: {}", vec3 )

    -- align text to the right
    fantasy.print( "{:>30}", "right aligned text" )

    -- centered text
    fantasy.print( "{:^30}", "centered text" )

    -- align text to the left
    fantasy.print( "{:<30}", "left aligned text" )

    -- display "a, b, c"
    fantasy.print( "{0}, {1}, {2}", 'a', 'b', 'c' )

    -- display "c, b, a"
    fantasy.print( "{2}, {1}, {0}", 'a', 'b', 'c' )

    -- display "abracadabra"
    fantasy.print( "{0}{1}{0}", "abra", "cad" )

    -- random number and floating precision output
    math.randomseed( os.time( ) )
    local random_integer = math.random( 0, 500 )
    local random_float = math.random()
    fantasy.print( "random_int: {} | random_float (rounded): {:.2f} | random_float (not rounded): {} ",
        random_integer,
        random_float,
        random_float
    )
end

return print_test
```

Output:
```
[print_test.lua] Hello World
[print_test.lua] My favorite number is 1337
[print_test.lua] vec3: vector: 10, 20, 30
[print_test.lua]             right aligned text
[print_test.lua]         centered text         
[print_test.lua] left aligned text             
[print_test.lua] a, b, c
[print_test.lua] c, b, a
[print_test.lua] abracadabra
[print_test.lua] random_int: 404 | random_float (rounded): 0.63 | random_float (not rounded): 0.63287926 
```

------------

## ```async```
### Type
`function`

### Description
Executes code away from the main worker thread. The `callback` function is optional and should be used if you're waiting for an indicator for this function to end. If you return a value in your function, the `callback` will pass the value back. See examples.

### Parameters
- `function` code
- `function` callback (optional)

### Returns
- `any`

### Example
```lua
local async = {}

function async.on_loaded()

    -- 1st
    fantasy.print( "hello world #1" )

    -- call async function
    fantasy.async(

        -- function/code we want to call
        function()
            -- 3rd
            fantasy.print( "hello world #3" )
        end
    )

    -- 2nd
    fantasy.print( "hello world #2" )

end

return async
```

### Example (Callback)
```lua
local async = {}

function async.on_loaded()

    -- normal
    fantasy.print( "hello world #1" )

    -- call async function
    fantasy.async(

        -- function/code we want to call (return value optional)
        function()
            fantasy.print( "hello world has been printed later #3" )
            return 1337
        end,

        -- output/result IF we are returning or looking for a callback once our async is completed (optional)
        function(result)
            fantasy.print("secret number: {}", result) -- should be 1337
        end
    )

    -- done
    fantasy.print( "hello world #2" )

end

return async
```

### Example (FC2 Functions)
```lua
local async = {}

function async.on_loaded()

    -- normal
    fantasy.print( "hello world #1" )

    -- call async function
    fantasy.async(

        -- function/code we want to call (return value optional)
        function()
            return fantasy.http():get("https://httpbin.org/headers")
        end,

        -- output/result IF we are returning or looking for a callback once our async is completed (optional)
        function(result)
            fantasy.print("headers: {}", result) -- should contain your http request headers
        end
    )

    -- done
    fantasy.print( "hello world #2" )

end

return async
```

### Example (Arguments and Multiple Return)
```lua
local async = {}

function async.on_worker()

    -- normal
    fantasy.print( "hello world #1" )

    -- call async function
    fantasy.async(

        -- function/code we want to call
        function( a, b, c )
            fantasy.print( "hello world #3 {} {} {}", a, b, c ) -- "hello world #3 apples oranges bananas
            return "dogs", "cats", "chickens"
        end,

        -- result
        function( e, f, g )
            fantasy.print("hello world #4 {} {} {}", e, f, g ) -- "hello world #4 dogs cats chickens
        end,

        -- arguments
        "apples", "oranges", "bananas"
    )

    -- done
    fantasy.print( "hello world #2" )

end

return async
```

------------

## ```wait```
###Type
`function`

###Description
Stops the current worker from continuing until a key is pressed in console.

------------

## ```exit```
###Type
`function`

###Description
Closes the FC2 solution.

------------

## ```sleep```
###Type
`function`

###Description
Sets the current callback to sleep for X amount of ms.

###Parameters
- `number` ms

------------

## ```calibrate```
###Type
`function`

###Description
Sets the calibration flag of an FC2 solution to `true`. Overlays will not work unless this calibration flag has been set.

###Returns
- `boolean`

------------

## ```is_calibrated```
###Type
`function`

###Description
Checks if the process is calibrated.

###Returns
- `boolean`

------------

## ```time```
###Type
`function`

###Description
Current time in ms.

###Returns
- `number`

------------

## ```terminal```
###Type
`function`

###Description
Executes a command in terminal/console and returns the result.

By enabling `no_logger`, you can prevent this method from displaying the terminal command in the logger. This can be useful for scripts that call `fantasy.terminal` consistently in the worker.

###Parameters
- `string` command
- `boolean` multithread (optional)
- `boolean` no_logger (optional)
- `function` callback (optional - only if `multithread` is `true`)

###Returns
- `string|nil`

### Example (callback/multithread)
```lua
-- Linux example. Replace cmd with "timeout /t 5 >nul && echo hello world" for Windows.
-- this should make "hello world" in terminal after 5 seconds on Linux.
local timeout = {}

function timeout.on_loaded()

    -- clock time when script launched
    fantasy.print("time on loaded: {}", os.clock())

    -- execute terminal command, response callback triggered when completed
    fantasy.terminal(
        "sleep 5 && echo hello world",  -- cmd
        true,                           -- multithread
        false,                          -- no logging
        function( output )              -- multithreaded response
            fantasy.print("callback clock time: {} | result: {}", os.clock(), output )
        end
    )

    -- clock time when on_loaded is done
    fantasy.print("time on finish loaded: {}", os.clock() )

end

return timeout
```

------------

## ```terminalu```
###Type
`function`

###Description
Executes a command in terminal/console and returns the result. This function differs from `terminal` as this one executes as a non-root user. This function only works for Linux.

###Parameters
- `string` command
- `boolean` multithread (optional)
- `function` callback (optional - only if `multithread` is `true`)

###Returns
- `string|nil`

------------

## ```terminalr```
###Type
`function`

###Description
Executes a command in terminal/console but doesn't wait to read the result. Both `terminal` and `terminalu` will only finish after the command output has been read. This function does not do that.

###Parameters
- `string` command
- `boolean` multithread (optional)

###Returns
- `string|nil`

------------

## ```set_worker```
###Type
`function`

###Description
This does **not** change the worker speed of an individual script. Read more about this [here (click me)](https://constelia.ai/forums/index.php?threads/worker-speed-locked-to-64-ticks-second.8674/#post-67306).

###Parameters
- `number` milliseconds

------------

## ```get_worker```
###Type
`function`

###Returns
- `table`
  - `number` speed
  - `number` ms
  - `number` tick

------------

## ```get_callback```
###Type
`function`

###Description
Gets the last callback the Lua module triggered.

###Returns
- `string`

------------

## ```notification```
###Type
`function`

###Description
This will create a notification based on your OS. Make sure you have a notification daemon installed on your Linux distro. On Windows, assure you have your Toast notifications enabled.

###Parameters
- `string` title
- `string` message

###Example
```lua
fantasy.notification( "FC2 ROBOT", "Hello World" )
```

------------

## ```overlay```
###Type
`function`

###Description
This will make the `overlay` module request to copy another window and create an overlay for it.

If `force` is passed as `true`, the overlay will start regardless of your settings.

###Parameters
- `string` target_window
- `boolean` force (optional)

###Example
```lua
fantasy.overlay( "Team Fortress 2" )
```

------------

## ```protection```
###Type
`function`

###Description
This will force set the protection mode for the user. This can reset if Sessions is recalibrated.

The `number` parameter accepts the following:

1: Standard Protection

2: Zombie

3: Kernel

Minimum mode cannot be activated with this function. Attempting to use any other values will create unwanted results.

###Parameters
- `number`

------------

## ```is_wayland```
### Type
`function`

### Returns
- `boolean`

------------

## ```skip_render_tick```
### Type
`function`

### Description
This will make FC2 skip the next rendering tick. This is useful if you don't want FC2 to draw anything on your screen for this specific `on_worker` tick.

------------

## ```prompt```
### Type
`function`

### Description
Prompts user in terminal/console to input a value. Useful if you want the member to manually input a value.

### Parameters
- `string` prompt

### Returns
- `string`

### Example
```lua
local prompt = {}

function prompt.on_loaded( )

    -- prompt user in terminal/console to input something
    local secret_password = fantasy.prompt("What's your secret password? ")

    -- print output. should be whatever the user put in.
    fantasy.print( secret_password )

    -- read results
    fantasy.wait()
end

return prompt
```

------------

## ```flush```
### Type
`function`

### Description
This function flushes the buffered output from console immediately. This is useful if you're creating a tool or FC2T project that reads what is displayed in terminal/console.

FC2 does not immediately flush buffer when output is displayed in terminal/console. Therefore, external programs reading from FC2 may not immediately read what is displayed. This function will resolve that, but will need to be called consistently if you wish to constantly read buffer.

------------

## ```to_linux```
### Type
`function`

### Description
This function allows you to execute code based on the OS. This is better than having to constantly do `fantasy.os`. If a Windows user calls `fantasy.to_linux` for example, the response is immediately `nil`. Performance will not be affected.

### Parameters
- `function`

### Example
```lua
fantasy.to_linux(
      function( )
            fantasy.terminal( fantasy.fmt( "chmod +x \"{}\"", file_path ) )
      end
)
```

------------

## ```to_windows```
### Type
`function`

### Description
This function allows you to execute code based on the OS. This is better than having to constantly do `fantasy.os`. If a Windows user calls `fantasy.to_windows` for example, the response is immediately `nil`. Performance will not be affected.

### Parameters
- `function`

------------

## ```to_os```
### Type
`function`

### Description
This function allows you to execute code based on the OS. This is better than having to constantly do `fantasy.os`. If a Windows user calls `fantasy.to_windows` for example, the response is immediately `nil`. Performance will not be affected.

### Parameters
- `function`
- `function`

### Example
```lua
local file_name = fantasy.to_os(
    
    -- windows
    function( )
        return "fantasy.troubleshooter3.exe"
    end,

    -- linux
    function( )
        return "fantasy.troubleshooter3.out"
    end

)
```

------------

## ```set_color```
###Type
`function`

###Description
Sets the color code based on a string identifier. Refer to this list for color codes [here](ttps://gist.github.com/JBlond/2fea43a3049b38287e5e9cefc87b2124).

### Parameters
- `string` identifier
- `string` code

### Example
```lua
fantasy.set_color( "[wayland_overlay.lua]", "\027[33;1m" )
```

------------

## ```popup```
###Type
`function`

###Description
Displays a pop-up

### Parameters
- `string` title
- `string` message
- `boolean` yesnocancel (Yes/No/Cancel dialog. If this is false, the dialog is only Yes/No)

### Returns
- `number` (0 = No, 1 = Yes, 2 = Cancel/Closed)

------------

## ```set_max_frames```
###Type
`function`

###Description
This is `max_rendering_frames`, except for a specific Lua script.

### Parameters
- `number`

---