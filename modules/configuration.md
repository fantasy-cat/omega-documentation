# configuration

## ```dump```
###Type
`function`

###Description
Dumps the JSON buffer to the logger and to console. The JSON buffer is beautified.

------------

## ```to_file```
###Type
`function`

###Description
Dumps the JSON buffer to a file. You can choose to beautify the content or not.

###Parameters
- `string` file
- `boolean` beautify?

------------

## ```save```
###Type
`function`

###Description
Saves your configuration to cloud.

------------

## ```load```
###Type
`function`

###Description
Reloads your configuration from cloud.

------------

## ```get```
###Type
`function`

###Parameters
- `MEM_` type
- `string` script_name
- `string` object_name

###Returns
- value

------------

## ```set```
###Type
`function`

###Parameters
- `MEM_` type
- `string` script_name
- `string` object_name
- value

###Returns
- value

------------

## ```overwrite```
###Type
`function`

###Description
This function will overwrite the local configuration inside of an FC2 solution. The local configuration is stored in JSON format. This function is useful for synchronizing configuration.

###Parameters
- `string` json

------------

## ```get_local```
###Type
`function`

###Description
Gets the local configuration JSON. This will soon replace the `buffer` string that is passed.

###Returns
- `string` json

------------