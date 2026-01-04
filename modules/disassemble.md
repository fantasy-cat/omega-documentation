# disassemble

`fantasy.disassemble( address [number] )` allows script developers to disassemble a specific address via a runtime debugger. This is useful for:

- Debugging and reverse engineering games or developing cheats using Omega.

- Debugging Lua scripts that use [icode]module:pattern[/icode] and find hardcoded offsets breaking easily.

- Iterating virtual tables (VTables).

- Verify runtime signature of other software; which is what an older version of Whitehat did to detect internal cheats.

x64dbg and ReClass obviously do something similar.

## Returns
- `table`
    - `string` mnemonic
    - `string` text
    - `number` address
    - `address` next
    - `number` size

## Example
![](https://i.imgur.com/GMK7vIB.png)

```lua
local modules = require( "modules" ) -- lib_modules
local disassemble_test = {}

function disassemble_test.on_worker( is_calibrated )

    -- not calibrated
    if not is_calibrated then return end

    -- get localplayer (current pointer)
    local localplayer = modules.entity_list:get_localplayer( )
    if not localplayer then return end

    -- 15 is the architectural hard limit for x86-64 processors 
    local max_instructions = 15
    local count = 0

    -- drawing settings
    local start_x = 1100
    local start_y = 10
    local line_height = 14
    local color_white = color:new( 255, 255, 255, 255 )

    -- loop through each instruction
    while count < max_instructions do

        -- use fantasy.disassemble to break down the instructions
        local instruction = fantasy.disassemble( localplayer )
        if not instruction then break end

        -- draw current instruction
        modules.kernel:text(
            instruction.text,
            14,
            start_x,
            start_y + ( count * line_height ),
            color_white
        )

        -- something returned in this instruction, just cut it off here.
        if instruction.mnemonic == "RET" then break end

        -- jump to the next instruction
        localplayer = instruction.next
        count = count + 1
    end

end

return disassemble_test
```