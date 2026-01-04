# engine.process

## ```set```
###Type
`function`

### Description
This is NOT intended to be used to check if a process is open. This function will make Omega attach to a target process. Thereby opening its hacking library to the process. You **need** to call this before calling other functions in this module. The only exception is when you are using `constellation.lua`, as it automatically attaches to a process already.

### Parameters
- `string` process name

### Returns
- `boolean

------------

## ```get_module```
###Type
`function`

###Description
This will load the information about a module into memory. This will allow you to use the module for hacking purposes.

###Parameters
- `string` name
- `number` segment (optional - linux only)

###Returns
- `module`

------------

## ```get_base```
###Type
`function`

###Description
Gets the base address of a process.

###Returns
- `address`

------------

## ```pattern```
### Type
`function`

### Description
Signature scanning.

### Parameters
- `string` module
- `string` signature
- `number` segment (linux only - pass `0` on Windows)
- `boolean` x64
- `boolean` relative
- `number` extra

## Returns
- `address`

---

## ```read```
###Type
`function`

### Description
Same as `address:read`.

------------

## ```monitor```
###Type
`function`

###Description
This will make FC2 monitor the status of a process. Multiple processes can be monitored at once. This is useful to check if a process closed.

###Parameters
- `string` name

------------

## ```get_name```
###Type
`function`

###Returns
- `string` name of process

------------

## ```get_game```
###Type
`function`

###Returns
- `GAME_ID`

------------

## ```list```
###Type
`function`

###Description
Lists all running processes.

###Returns
- `table`
    - `string` name
    - `number` id

------------

## ```get_modules```
###Type
`function`

###Returns
- `table` table of `module` class instances.

------------

## ```create```
###Type
`function`

### Description
Creates a subprocess attached to the main solution. It is recommended to use this so that when the solution closes, any subprocess also closes.

If you do not wish to pass launch arguments, simply provide an empty `string`.

###Parameters
- `string` (path)
- `string` (args)

------------

## ```is_open```
###Type
`function`

###Parameters
- `string`

###Returns
- `boolean`

------------