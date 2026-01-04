# fantasy (modules)

## ```cryptography```
###Type
`function`

###Returns
- `module`

------------

## ```scripts```
###Type
`function`

###Returns
- `module`

------------

## ```input```
###Type
`function`

###Returns
- `module`

------------

## ```configuration```
###Type
`function`

###Returns
- `module`

------------

## ```steam```
###Type
`function`

###Returns
- `module`

------------

## ```file```
###Type
`function`

###Returns
- `module`

------------

## ```engine.entity_list```
###Type
`function`

###Returns
- `module`

------------

## ```engine.bsp```
###Type
`function`

###Returns
- `module`

------------

## ```engine.process```
###Type
`function`

###Returns
- `module`

------------

## ```engine.source```
###Type
`function`

###Returns
- `module`

------------

## ```engine.render```
###Type
`function`

###Returns
- `module`

------------

## ```engine.kernel```
###Type
`function`

###Returns
- `module`

------------

## ```engine.w2s```
###Type
`function`

### Description
This function not only returns the World2Screen, but it also returns the `width` and `height` of the calibrated game window.

The `width`, and `height` of the game window will still be passed even if this function fails. Meaning, if the `vector` provided is out of screen and would return `nil`, the `width`, and `height` values are still provided.

`width` and `height` will only be 0 if FC2 is calibrated to a game that isn't officially supported.

You can actually pass `nil` as a parameter to simply get the `width` and `height` values.

###Parameters
- `vector`

###Returns
- `vector`
- `number` width
- `number` height

------------

## ```constelia```
###Type
`function`

###Returns
- `module`

------------

## ```http```
###Type
`function`

###Returns
- `module`

------------

## ```achievements```
###Type
`function`

###Returns
- `module`

------------

## ```window```
###Type
`function`

### Parameters
- `string` window_name/window_class

###Returns
- `module`

------------

## ```fonts```
###Type
`function`

###Returns
- `module`

------------