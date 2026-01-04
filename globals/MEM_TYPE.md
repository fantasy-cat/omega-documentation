# MEM_TYPE

MEM_TYPE is a helper global used in functions like `address:read` (for reading memory values) and `configuration:get` (for retrieving config settings). It defines a set of constants (starting with `MEM_`) that specify the data type you're working with. These originated from earlier versions of FC2, and some might seem outdated or overlapping now. The key idea is that these constants tell Omega how to interpret and convert data correctly before passing it to Lua, where your scripts run.

In short: You use a `MEM_` constant to describe what kind of value you're expecting or handling. Omega then processes it and converts it into a Lua-friendly format.

| MEM         | Lua Equivalent Type/Class |
|-------------|---------------------------|
| MEM_BOOL    | boolean                   |
| MEM_FLOAT   | number                    |
| MEM_INT     | number                    |
| MEM_STRING  | string                    |
| MEM_VECTOR  | vector                    |
| MEM_SHORT   | number                    |
| MEM_DOUBLE  | number                    |
| MEM_DATA    | address                   |
| MEM_ADDRESS | address                   |
| MEM_BYTE    | number                    |
| MEM_LONG    | number                    |
