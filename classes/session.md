# session

The table contains the same data returned from the `getMember` Web API function. In addition, it passes a `license` `string`, which contains your raw license key. Furthermore, it contains the following functions:

## ```api```
### Type
`function`

### Description
Calls a Web API function where the `key` parameter is automatically fulfilled. This only sends a `GET` request. You would need to use `http:post` to send a `POST` request.

### Parameters
- `string` function

### Returns
- `string`

### Example
```lua
local result = fantasy.session:api( "getMember" )
```

---

## ```has_perk```
### Type
`function`

### Description
Checks if a member has a certain perk.

### Parameters
- `number` perk_id

### Returns
- `boolean`

---

## ```get_perks```
### Type
`function`

### Description
Gets all perks. Formatted like `getMember` formats it (by id and time unlocked).

### Returns
- `table`

---

## ```get_scripts```
### Type
`function`

### Description
Gets all scripts enabled on cloud. This returns a `table` of `script` class instances.

### Returns
- `table`

---