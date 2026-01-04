# on_process_fail

## Description
This callback is called when Omega fails to execute code in the `os` module.

## Parameters
- `number` code (`PROCESS_FAIL_CODE_*`)
- `string` message

## Example
```lua
function my_script.on_process_fail( code, message )
    if code == PROCESS_FAIL_CODE_SET_PROCESS then
        fantasy.log( "omega could not gain access to the process." )
    end
end
```