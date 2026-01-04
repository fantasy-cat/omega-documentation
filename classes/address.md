# address

## ```is_valid```
### Type
`function`

### Description
Checks if the address assigned to this class is valid.

### Returns
- `boolean`

---

## ```iz_zero```
### Type
`function`

### Description
Checks if the address assigned to this class is zero or not. `is_valid` is not implied.

### Returns
- `boolean`

---

## ```read```
### Type
`function`

### Description
Reads a memory address.

### Parameters
- `MEM_TYPE`
- `address/number`
- `number` Optional parameter for `string` length (`MEM_STRING` only).

### Returns
- `any` Based on `MEM_TYPE`.

---

## ```write```
### Type
`function`

### Description
Writes a value to a memory address. This function does not work unless `system.lua:allow_memory_writing_operations` is enabled (which is disabled by default). Therefore, Omega scripts will never have permission to write to game memory unless you strictly and specifically give it permission to.

Consider using this for making cheats for games that aren't strongly protected. If you're making a trainer or a simple cheat for a random game, this can be useful.

### Parameters
- `MEM_TYPE`
- `address/number`
- `any` The value to write (type depends on `MEM_TYPE`).

### Returns
- `nil`

---

## ```add```
### Type
`function`

### Description
Adds an address to this address.

### Parameters
- `address/number`

### Returns
- `address`

---

## ```subtract```
### Type
`function`

### Description
Subtracts an address to this address.

### Parameters
- `address/number`

### Returns
- `address`

---

## ```bor```
### Type
`function`

### Description
Bitwise `OR` operation with this address and a value.

### Parameters
- `number`

### Returns
- `boolean`

---

## ```band```
### Type
`function`

### Description
Bitwise `AND` operation with this address and a value.

### Parameters
- `number`

### Returns
- `boolean`

---

## ```rshift```
### Type
`function`

### Description
Right shift bitwise operation with this address and a value.

### Parameters
- `number`

### Returns
- `boolean`

---

## ```lshift```
### Type
`function`

### Description
Left shift bitwise operation with this address and a value.

### Parameters
- `number`

### Returns
- `boolean`

---