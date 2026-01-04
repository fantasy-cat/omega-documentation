# color

## ```r```
###Type
`float`

------------

## ```g```
###Type
`float`

------------

## ```b```
###Type
`float`

------------

## ```a```
###Type
`float`

------------

## ```new```

### Type
`function`

### Description
Creates a new color class. You can either send a RGBA hex value or individual RGBA bytes.

### Parameters
- `number` r
- `number` g
- `number` b
- `number` a

or

- `string` hex

### Returns

- `color`

### Example
```lua
local red = color:new( 255, 0, 0, 255 )
local red2 = color:new( "FF0000FF" )
```

------------