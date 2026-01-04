# window

## ```address```

### Type

`userdata`

------------

## ```get_id```

### Type
`function`

### Description
On Windows, this would return the HWND of a window as a number. 

On Linux, this returns the window ID as a number.

### Returns
- `number`

------------

## ```get_dimensions```

### Type
`function`

### Description
This gets the dimensions of a window, including its position on the monitor.

### Returns
- `table`
    - `number` left
    - `number` top
    - `number` right
    - `number` bottom

------------

## ```is_focused```

### Type
`function`

### Returns
- `boolean`

------------

## ```bypass_compositor```

### Type
`function`

### Description
Bypasses compositor restrictions on window (Linux only)

### Returns
- `boolean`

------------
