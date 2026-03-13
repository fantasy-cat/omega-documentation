# address

## ```new```

### Type
`function`

### Description
Creates a new address class. You can either send a number, lightuserdata, or table containing an `address` field.

### Parameters
- `number/userdata/table` address

### Returns

- `address` ([ref](https://constelia.ai/sdk/Omega/classes/address/))

### Example
```lua
-- process:get_base only returns a lightuserdata. Convert it to an address class.
local base_address = address:new( modules.process:get_base( ) )
```

------------