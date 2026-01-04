# on_kernel_driver_load

## Description
This callback is called when a kernel driver is loaded.

## Parameters
- `string` name

## Example
```lua
function my_script.on_kernel_driver_load( name )
    fantasy.log( "kernel driver loaded: {}", name )
end
```