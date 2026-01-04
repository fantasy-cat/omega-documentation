# on_http_request

## Description
This callback is called when a request is made to the HTTP server.

## Parameters
- `table`
    - `string` ip
    - `number` port
    - `string` method
    - `string` path
    - `string` body
    - `table` params

## Returns
- Returning a `string` will send a `string` back to the requester.

## Example
```lua
function my_script.on_http_request( data )
    if data.path == "/luar" then
        return "Hello World!"
    end
end
```

## Methods

<!-- TOC -->
  * [```/lua```](#lua)
  * [```/sessions```](#sessions)
  * [```/configuration```](#configuration)
  * [```/configuration```](#configuration-1)
  * [```/reset```](#reset)
  * [```/directory```](#directory)
  * [```/processes```](#processes)
  * [```/ping```](#ping)
  * [```/achievements```](#achievements)
  * [```/ipc```](#ipc)
  * [```/shutdown```](#shutdown)
  * [```/luar```](#luar)
  * [```/luar```](#luar-1)
  * [```/reload```](#reload)
<!-- TOC -->

## ```/lua```
###Type
`GET Method`

###Description
This will run Lua code inside of a specific script. You can leave the `script` parameter blank. If you do, FC2 will automatically use `fc2.lua`, which is automatically loaded upon launch. `code` must be URI encoded.

Read [this](https://fantasy.cat/forums/index.php?threads/intercommunication-http-lua.7640/) guide on HTTP <-> Lua intercommunication.

###Parameters
- `script` script_name
- `code` lua_code

------------

## ```/sessions```
###Type
`GET Method`

###Description
This will return a JSON object of the member's Session data. This will also include the member's raw license key. This is similar to `getMember` in the Web API.

------------

## ```/configuration```
###Type
`GET Method`

###Returns
- `json` configuration

------------

## ```/configuration```
###Type
`POST Method`

###Description
This will set the configuration inside of FC2. This will not save it in the cloud network.

###Parameters
- `json` configuration

------------

## ```/reset```
###Type
`GET Method`

###Description
Reloads all scripts and the solution.

------------

## ```/directory```
###Type
`GET Method`

###Description
This will list all files in a directory. If you do not pass `path` then FC2 will use your current directory.

###Parameters
- `path` directory path (optional)

------------

## ```/processes```
###Type
`GET Method`

###Description
Gets a list of all currently running processes.

------------

## ```/ping```
###Type
`GET Method`

###Returns
- `pong`

------------

## ```/achievements```
###Type
`GET Method`

###Returns
- `json` achievement data

------------

## ```/ipc```
###Type
`GET Method`

###Description
This will automatically install ZombieFC2 or FC2K depending on the protection level of the member.

------------

## ```/shutdown```
###Type
`GET Method`

###Description
Closes a solution.

------------

## ```/luar```
###Type
`GET Method`

###Description
This will trigger an alternative version of the `on_http_request` callback, in which you can return a `string`. The `string` value returned is sent back to the client/browser that made the HTTP request. [Click me for an example](https://constelia.ai/forums/index.php?threads/luar-run-lua-code-read-results-on-client-browser.9528/).

------------

## ```/luar```
###Type
`POST Method`

###Description
This will trigger an alternative version of the `on_http_request` callback, in which you can return a `string`. The `string` value returned is sent back to the client/browser that made the HTTP request. [Click me for an example](https://constelia.ai/forums/index.php?threads/luar-run-lua-code-read-results-on-client-browser.9528/). The difference between this method and `GET` is that this method contains a body.

------------

## ```/reload```
###Type
`GET Method`

###Parameters
- `script` script name

###Description
Allows you to reload a single script instead of constantly having to reload all scripts/restart solution.

------------