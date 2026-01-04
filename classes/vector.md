# vector

## ```x```

### Type

`float`

------------

## ```y```

### Type

`float`

------------

## ```z```

### Type

`float`

------------

## ```new```

### Type

`function`

### Description

Creates a new vector class.

### Parameters

- `number` x
- `number` y
- `number` z

### Returns

- `vector`

### Example
```lua
local vec3 = vector:new( 5.0, 10.0, 15.0 )
```

------------


## ```add```

### Type

`function`

### Description

Adds two vectors.

### Parameters

- `vector` other_vector

### Returns

- `vector`

------------

## ```subtract```

### Type

`function`

### Parameters

- `vector` other_vector

### Returns

- `vector`

------------

## ```multiply```

### Type

`function`

### Parameters

- `vector` other_vector

### Returns

- `vector`

------------

## ```divide```

### Type

`function`

### Parameters

- `vector` other_vector

### Returns

- `vector`

------------

## ```print```

### Type

`function`

### Description

This will print the `x`, `y`, and `z` values into console.

------------

## ```distance```

### Type

`function`

### Parameters

- `vector` other_vector

### Returns

- `number`

------------

## ```normalize```

### Type

`function`

### Returns
- `vector`

------------

## ```clamp```

### Type

`function`

### Returns
- `vector`

------------

## ```angle```

### Type

`function`

### Description

Calculates the angle of two vectors.

### Parameters

- `vector` other_vector

### Returns

- `vector`

------------

## ```forward```

### Type

`function`

### Returns

- `vector`

------------

## ```dot```

### Type

`function`

### Returns

- `vector`

------------

## ```fov```

### Type

`function`

### Description

Gets the FOV from one vector to another.

### Parameters

- `vector` other_vector

### Returns

- `number`

------------

## ```humanize```

### Type
`function`

### Description
This method will apply the Humanizer4 "humanize" module to a mouse X and Y destination. This is useful if you wish to automatically apply a dynamic algorithm used by Humanizer4, in which the mouse destination becomes humane depending on the assumption of your recent cursor movement.

This method will return `nil` under the following conditions:

- The position is outside a normal threshold. In a 3D world, certain distances make this method pointless, hence why it will return `nil`.
- This is called in a `on_humanizer_xxx` callback. Humanizer4 already applies this. This shouldn't be applied twice.
- If the `z` in your `vector` is anything but 0. This is only for pixel relocation. This is two-dimensional.

### Returns
- `vector`

------------

## ```is_zero```

### Type

`function`

### Description
If a vector is [0, 0, 0] (within tolerance).

### Returns

- `boolean`

------------

## ```scale```

### Type

`function`

### Description
Multiplies each field by a number.

### Parameters
- `number` scalar

### Returns
- `vector`

------------