# file

## ```write```
###Type
`function`

###Parameters
- `string` file
- `string` content

------------

## ```read```
###Type
`function`

###Parameters
- `string` file

###Returns
- `string` content

------------

## ```exists```
###Type
`function`

###Parameters
- `string` file

###Returns
- `boolean`

------------

## ```append```
###Type
`function`

###Parameters
- `string` file
- `string` content

------------

## ```copy```
###Type
`function`

###Parameters
- `string` source
- `string` destination

------------

## ```remove```
###Type
`function`

###Parameters
- `string` file

------------

## ```hash```
###Type
`function`

###Parameters
- `string` file

###Returns
- `string`

------------

## ```rename```
###Type
`function`

###Parameters
- `string` source
- `string` destination

------------

## ```is_empty```
###Type
`function`

###Parameters
- `string` file

###Returns
- `boolean`

------------

## ```create_directory```
###Type
`function`

###Parameters
- `string` path or `nested/path/like/this/on/linux` or `nested\\path\\like\\this\\on\\windows`

------------

## ```list```
###Type
`function`

###Description
Lists all files in directory as a nested table.

###Parameters
- `string` directory

###Returns
- `table`
    - `string` name
    - `string` raw_name
    - `string` extension
    - `string` directory
    - `string` relative
    - `string` parent
    - `boolean` is_directory
    - `boolean` has_extension

------------

## ```listr```
###Type
`function`

###Description
Same as `list` except it's recursive. 

------------

## ```fix_separators```
###Type
`function`

###Description
This fixes the pathing of a directory depending on the OS. On Windows, directories are separated by \\. This does not apply to other operating systems. If your script is working with file directories, it is best that this function is used to allow both Windows and Linux users the best peace of mind.

###Parameters
- `string` directory

###Returns
- `string`

------------

## ```current_directory```
###Type
`function`

###Description
You should use this function instead of using the session directory for pathing because dual booting fantasy.cat members will pathing issues. For example: If your Session directory on Windows is `C:\\Hello_World` and then you dual boot to use FC2 on Linux, obviously your Linux installation will not have that path. This is the same vice versa.

###Returns
- `string`

------------

## ```get_solution_directory```
### Type
`function`

### Description
This returns a table of all directories created by FC2. 

### Returns
- `table`
      - `string` directory 
      - `string` logs 
      - `string` lib_scripts 
      - `string` resources 
      - `string` disabled_scripts 
      - `string` core_scripts 
      - `string` scripts
      - `string` this (`/resources/script_name/`)

### Example
```lua
-- get file module
local file = fantasy.file()

-- get directories
local directories = file:get_solution_directory()

-- output to terminal
fantasy.log("My core scripts are at: {}", directories["core_scripts"] )
```

------------

## ```format```
### Type
`function`

### Description
This does the same thing as `fix_separators`. This function is simply named this way for flavor purposes.

------------

## ```checksum```
### Type
`function`

### Description
Returns the sha256 checksum of a file. This will return `nil` if the file does not exist.

### Parameters
- `string` file_path

### Returns
- `string|nil`

------------

## ```escape```
### Type
`function`

### Description
Automatically escapes backslashes of a Windows directory.

### Parameters
- `string` file_path

### Returns
- `string`

------------

## ```find```
### Type
`function`

### Description
Finds a file in a directory and its subdirectories.

### Parameters
- `string` folder
- `string` file_path

### Returns
- `string`

### Example
```lua
function test.on_loaded( )
    local steam = fantasy.steam( )
    local file = fantasy.file( )
    for key, value in pairs( steam:get_libraries() ) do
        fantasy.log( "{}: {}", key, value )
    end

    -- find cs2 directory in one of our steam libraries
    local cs2_path = steam:find( "Counter-Strike Global Offensive" )

    -- client.dll/libclient.so name based on OS
    local client_name = fantasy.to_os(

        -- windows
        function( )
            return "client.dll"
        end,

        -- linux
        function( )
            return "libclient.so"
        end
    )

    -- find it inside of cs2 directory and get its size.
    local client_path = file:find( cs2_path, client_name )
    local client_size = file:size( client_path )

    -- display
    fantasy.log( "cs2 path: {}", cs2_path )
    fantasy.log( "cs2:{} path: {} ({})", client_name, client_path, client_size )
end
```

------------

## ```size```
### Type
`function`

### Description
Gets a file size.

### Parameters
- `string` file_path

### Returns
- `number`

------------

## ```last_modified```
### Type
`function`

### Description
This will get the timestamp when a file was last modified. This is useful for detecting if a file was recently written to.

### Parameters
- `string` file_path

### Returns
- `number`

------------