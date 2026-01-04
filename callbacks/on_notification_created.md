# on_notification_created

## Description
This callback is called when any script uses `fantasy.notification`.

## Parameters
- `string` title
- `string` message

## Returns
- Returning `false` will prevent the notification from being created.

## Example
```lua
function my_script.on_notification_created( title, message )
    fantasy.log( "notification suppressed: {} - {}", title, message )
    return false
end
```