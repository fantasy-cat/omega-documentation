# steam

## ```get_accounts```
###Type
`function`

###Description
Gets all Steam accounts logged on your system. Returns this data as a nested `steam_account` table class.

###Return
- `table` steam_accounts

------------

## ```get_libraries```
###Type
`function`

###Description
Gets all library paths you have on your currently logged in Steam account. This is essentially the directories of your installed games. Returns this data as a nested `steam_library` table class.

###Return
- `table` steam_libraries

------------

## ```find```
###Type
`function`

###Description
Checks if you have a Steam game installed. Returns the full directory path. This is useful for BSP parsing or reading game files.

###Return
- `string` path

------------