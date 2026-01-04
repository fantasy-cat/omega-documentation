# constelia

## ```add_voice```
### Type
`function`

### Description
The argument provided must be a voiceline that was already hard-coded into the FC2 solution. The Constelia module actually shows you all the voicelines added by checking the logs. If the voiceline doesn't exist, then this function will not work.

### Parameters
- `string` voiceline

------------

## ```download```
### Type
`function`

### Description
This will download the voicelines from the server.

### Parameters
- `string` url
- `string` name_of_voiceline

------------

## ```chat```
### Type
`function`

### Description
Requires the perk "Bond Between Human and AI". This will send a request to AI.

### Parameters
- `string`

------------

## ```get_voicelines```
### Type
`function`

### Description
Gets a list of voicelines.

### Returns
- `table`

------------

## ```play_voice```
### Type
`function`

### Description
Play voiceline.

### Parameters
- `string` name_of_voiceline

------------

## ```humanizer_test```
### Type
`function`

### Description
Verify and update humanizer test results.

------------
