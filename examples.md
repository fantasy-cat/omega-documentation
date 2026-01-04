# examples

There are over 50 scripts available. For privacy reasons and out of respect for the community authors, more advanced and detailed scripts are not listed on this page. Verified members can access all script source codes.

<!-- TOC -->
* [examples](#examples)
  * [humanizer_logs.lua](#humanizer_logslua)
  * [head_dot.lua](#head_dotlua)
  * [demoman.lua](#demomanlua)
  * [my_cheat.lua (Standalone CS2 Triggerbot Cheat)](#my_cheatlua-standalone-cs2-triggerbot-cheat)
  * [battlebitlean.lua](#battlebitleanlua)
  * [spread_circle.lua](#spread_circlelua)
<!-- TOC -->

## humanizer_logs.lua
```lua
--[[
--  @title
--      humanizer_logs.lua
--
--  @author
--      typedef
--
--  @description
--      logs humanizer4 information to file and expands
--      current humanizer4 logs.
--]]
local modules = require( "modules" ) -- lib_modules

-- /sessions_directory/omega/resources/humanizer_logs/
local resources = modules.file:get_solution_directory().this

---@class humanizer_logs
---@field verbose boolean more details about humanizer
---@field to_normal_logs boolean send logs to normal constellation4 logs
---@field to_terminal boolean logs in terminal
---@field to_custom_file string to a custom file
---@field sort_by_date boolean if you have to_custom_file, the file will be sorted by date.
---@field exclude_zeroed boolean if 0, 0 mouse movement, don't log anything.
---@field append_to_custom function appends humanizer4 logs to custom file
local humanizer_logs =
{
    verbose = true,
    to_normal_logs = true,
    to_terminal = true,
    to_custom_file = "humanizer4.txt",
    sort_by_date = true,
    exclude_zeroed = true,

    append_to_custom = function( this, fmt )

        local path = ""

        if this.sort_by_date then
            path = fantasy.fmt(
                "{}{}_{}",
                resources,
                os.date("%Y-%m-%d"),
                this.to_custom_file
            )
        else
            path = fantasy.fmt(
                "{}{}",
                resources,
                this.to_custom_file
            )
        end

        modules.file:append(
            path,
            fantasy.fmt(
                "[{}] {}
",
                os.date("%Y-%m-%d %H:%M:%S"),
                fmt
            )
        )

    end
}

function humanizer_logs.on_loaded( )

     -- always create directory in case to_custom_file gets fulfilled.
    modules.file:create_directory( resources )
end

function humanizer_logs.on_humanizer( _, _, data )

    local fmt = ""

    -- "zeroed cursor movement saved"; don't log anything in this case. 
    if humanizer_logs.exclude_zeroed then
        if data.x == 0 and data.y == 0 then
            if humanizer_logs.exclude_zeroed then
                return
            end
        end
    end

    if humanizer_logs.verbose then
        fmt = fantasy.fmt( [[
Humanizer4 Activated:
    -> target: {}
    -> last target: {}
    -> bone: {}
    -> true_fov: {}
    -> static_fov: {}
    -> distance: {}
    -> angle: {}
    -> one tapping: {}
    -> destination: {}
    -> shots fired: {}
    -> x: {}
    -> y: {}
    -> pull: {}
]],
        data.entity,
        data.last_target,
        data.bone_id,
        data.true_fov,
        data.static_fov,
        data.distance,
        data.angle,
        data.is_one_tapping,
        data.bone,
        data.shots_fired,
        data.x,
        data.y,
        data.pull
    )
    else
        fmt = fantasy.fmt( [[
Humanizer4 Activated:
    -> bone: {}
    -> one tapping: {}
    -> destination: {}
    -> shots fired: {}
    -> x: {}
    -> y: {}
    -> pull: {}
]],
        data.bone_id,
        data.is_one_tapping,
        data.bone,
        data.shots_fired,
        data.x,
        data.y,
        data.pull
    )
    end

    if humanizer_logs.to_normal_logs then
        fantasy.log( "{}", fmt )
    end

    if humanizer_logs.to_terminal then
        fantasy.print( "{}", fmt )
    end

    if string.len( humanizer_logs.to_custom_file ) ~= 0 then
       humanizer_logs:append_to_custom( fmt )
    end

end

return humanizer_logs
```

## head_dot.lua
```lua
---[[
--- @title
---     Head Dot ESP
--- @author
---     cessna172
--- @description
---     Used for gathering information on enemy positions
---]]
local modules = require( "modules" ) -- lib_modules
local players = require( "players" ) -- lib_players
local keys = require( "keys" )       -- lib_keys

local head_dot =
{
    enabled = true,
    size = 5,
    colour = "FFFFFFFF",


    always_on = false,
    toggle_key = "ALT",

    cache =
    {
        gameid = nil,
    },

        draw_dot = function(self, entity)
        local bone = entity:get_bone(6)
        if not bone then return end

        local w2s = modules.w2s(bone)
        if not w2s then return end

        local clr = color:new(self.colour)
        local half_size = self.size / 2

        local x_pos = w2s.x - half_size
        local y_pos = w2s.y - half_size

        modules.kernel:boxf(x_pos, y_pos, self.size, self.size, clr)
    end,
}

function head_dot.on_worker(is_calibrated)

    if not is_calibrated or not head_dot.enabled then
        return
    end

    local should_draw_this_frame = head_dot.always_on or modules.input:is_key_down(keys.get_key(head_dot.toggle_key))

    if not should_draw_this_frame then
        return
    end

    if head_dot.cache.gameid ~= GAME_CS2 then return end

    local localplayer = players.to_player(modules.entity_list:get_localplayer())
    if not localplayer then return end

    for _, entity in pairs(modules.entity_list:get_enemies()) do
        local enemy_player = players.to_player(entity)

        if enemy_player and enemy_player:is_alive() then
            head_dot:draw_dot(enemy_player)
        end
    end
end

function head_dot.on_solution_calibrated(data)
    head_dot.cache.gameid = data.gameid
    if head_dot.cache.gameid ~= GAME_CS2 then
        fantasy.log("Head Dot: This script is designed for CS2 and will not run.")
    else
        fantasy.log("Head Dot: Script calibrated for CS2.")
    end
end

return head_dot
```

## demoman.lua
```lua
--[[
    @title
        DemoAIO

    @author
        typedef

    @description
        Demoman All-In-One features
--]]
local players = require( "players" ) -- lib_players
local modules = require( "modules" ) -- lib_modules

local demoman =
{
    -- auto det
    auto_det = true,
    auto_det_sensitivity = 7.0,
    auto_det_triggerbot = false,
    auto_det_triggerbot_key = 9,

    -- esp our stickies?
    esp = true,
    esp_color = "00FF00",
    esp_enemy = true,
    esp_color_enemy = "FF0000",

    -- no humanizer mode
    no_humanizer = true,

    -- cache
    cache = {},

    -- right click function so I dont have to repeat my code
    right_click = function( self )

        -- boom
        if fantasy.os == "linux" then
            modules.input:click( 3 ) -- On Linux, Button3 is right click for some reason.
        else
            modules.input:click( 2 )
        end

    end
}

function demoman.on_humanizer_pre( localplayer )

    -- recast to lib_players
    localplayer = players.to_player( modules.entity_list:get_localplayer() )
    if not localplayer then return end

    -- are we a demoman and have no_humanizer on?
    return not (localplayer:get_tf2_class() == TF2_DEMOMAN and demoman.no_humanizer)
end

function demoman.on_solution_calibrated( solution )

    -- this script only works for TF2.
    if solution[ "gameid" ] ~= GAME_TF2 then return false end
end

function demoman.on_worker()

    -- empty stickies table for esp
    demoman.cache.stickies = {}
    demoman.cache.enemy_stickies = {}

    -- not calibrated
    if not fantasy.is_calibrated() then return end

    -- get localplayer
    local localplayer = players.to_player( modules.entity_list:get_localplayer() )
    if not localplayer then return end

    -- are we alive?
    if not localplayer:is_alive() then return end

    -- are we a demoman?
    if localplayer:get_tf2_class() ~= TF2_DEMOMAN then return end

    -- loop through all entities
    for _, entity in pairs( modules.entity_list:get_all_entities() ) do

        -- is dormant?
        if entity:is_dormant() then goto continue end

        -- get the person who threw this entity (if someone actually can throw them)
        local thrower = entity:read( MEM_INT, modules.source:get_netvar( "DT_TFProjectile_Throwable", "m_hThrower" ) )
        if thrower == 0 then goto continue end

        -- get handle from entity
        thrower = modules.entity_list:from_handle( thrower )
        if not thrower then goto continue end

        -- check the projectile/nade type
        local nade_type = entity:read( MEM_INT, modules.source:get_netvar( "DT_TFProjectile_Pipebomb", "m_iType" ) )
        if nade_type ~= 1 then goto continue end -- 1 = sticky

        -- get the thrower's team, is this a teammate or enemy?
        if thrower:read( MEM_INT, modules.source:get_netvar( "DT_BasePlayer", "m_iTeamNum" ) ) ~= localplayer:get_team() then

            -- is our enemy esp enabled?
            if demoman.esp_enemy then
                local box = entity:get_box_dimensions()
                if box ~= nil then

                    table.insert(demoman.cache.enemy_stickies, box )

                    modules.kernel:box( box["left"] - 3, box["top"] - 3, box["right"] + 8, box["bottom"] + 8, 1, color:new( demoman.esp_color_enemy ) )

                end
            end

            -- we're done here with this entity because it's clearly not ours, so we don't need to continue auto-det logic.
            goto continue
        end

        -- did we throw this sticky?
        if thrower["address"] ~= localplayer["address"] then goto continue end

        -- we have a sticky down and this entity appears to be that. let's cache it's position.
        local position = entity:read( MEM_VECTOR, modules.source:get_netvar( "DT_BasePlayer", "m_vecOrigin" ) )

        -- do we have esp enabled? store our stickes
        if demoman.esp then
            local box = entity:get_box_dimensions()

            if box ~= nil then
                table.insert(demoman.cache.stickies, box )

                modules.kernel:box( box["left"] - 3, box["top"] - 3, box["right"] + 8, box["bottom"] + 8, 1, color:new( demoman.esp_color ) )
            end
        end

        -- do we have auto-det enabled? if not, we're done with this entity.
        if not demoman.auto_det then goto continue end

        -- so now we have our sticky position, let's see who is near it.
        for _, player in pairs( modules.entity_list:get_enemies() ) do

            -- dormant
            if player:is_dormant() then goto continue_player end

            -- get their origin
            local origin = player:read( MEM_VECTOR, modules.source:get_netvar( "DT_BasePlayer", "m_vecOrigin" ) )
            if not origin then goto continue_player end

            -- get the distance between the sticky and the enemy
            local distance = origin:distance( position )

            -- are they in our sensitivity range?
            if distance > demoman.auto_det_sensitivity then goto continue_player end

            -- no triggerbot? just boom
            if not demoman.auto_det_triggerbot then

                demoman:right_click()
            else


                -- triggerbot is enabled, so is our key down?
                if modules.input:is_key_down( demoman.auto_det_triggerbot_key ) then

                    demoman:right_click()
                end
            end

            ::continue_player::
        end

        ::continue::

    end

end

return demoman
```


## my_cheat.lua (Standalone CS2 Triggerbot Cheat)
```lua
local modules = require( "modules" ) -- lib_modules
local json    = require( "json" ) -- lib_json
local my_cheat =
{

    cache =
    {
        client = nil,
        patterns = nil,
        schemas = nil,
    }
}

function my_cheat.on_loaded( )

    --[[
    --  find cs2.exe
    --  obviously we can't do any memory operations if the game isn't open to begin with
    --]]
    if not modules.process:is_open( "cs2.exe" ) then
        fantasy.log( "cs2 is not open" )
        return false
    end

    --[[
    --  constellation is already enabled
    --  don't run two cheats at once. 
    --
    --  if you ignore this, both cheats will run and can create performance issues or compatibility issues
    --  this is also an issue with aurora
    --]]
    if modules.configuration:get( MEM_BOOL, "constellation.lua", "enabled" ) then
        fantasy.log( "constellation is enabled" )
        return false
    end

    if modules.configuration:get( MEM_BOOL, "aurora.lua", "enabled" ) or modules.kernel:is_aurora_loaded( ) then
        fantasy.log( "aurora is enabled/loaded" )
        return false
    end

    --[[
    --  this tells omega/fc2.5 to focus on a specific process
    --  this will also automatically set fc2k or rootlink
    --]]
    if not modules.process:set( "cs2.exe" ) then
        fantasy.log( "process could not be set")
        return false
    end

    --[[
    --  let's get the client.dll module
    --  we're going to need it for memory operations
    --]]
    my_cheat.cache.client = modules.process:get_module( "client.dll" )
    if not my_cheat.cache.client then
        fantasy.log( "client.dll not found" )
        return false
    end

    --[[
    --  let's directly download from https://github.com/a2x/cs2-dumper/blob/main/output/offsets.json
    --  after doing so, we will parse the JSON data automatically
    --]]
    local response = modules.http:get( "https://raw.githubusercontent.com/a2x/cs2-dumper/refs/heads/main/output/offsets.json" )
    if not response then
        fantasy.log( "could not fetch offsets.json" )
        return false
    end

    my_cheat.cache.patterns = json.decode( response )
    if not my_cheat.cache.patterns then
        fantasy.log( "fetched offsets.json is not a valid json" )
        return false
    end

    --[[
    --  let's do the same, except with schemas
    --]]
    response = modules.http:get( "https://raw.githubusercontent.com/a2x/cs2-dumper/refs/heads/main/output/client_dll.json" )
    if not response then
        fantasy.log( "could not fetch client_dll.json schemas" )
        return false
    end

    my_cheat.cache.schemas = json.decode( response )
    if not my_cheat.cache.schemas then
        fantasy.log( "client_dll.json is invalid" )
        return false
    end

    --[[
    -- we're going to later use the entity list in `on_worker`. let's just get the address now instead of calculating it
    -- every tick
    --]]
    my_cheat.cache.entity_list = my_cheat.cache.client:read(
        MEM_ADDRESS,
        my_cheat.cache.patterns[ "client.dll" ][ "dwEntityList" ]
    )

    --[[
    -- let's leave a debug message for our progress so far
    --]]
    fantasy.log( "client.dll: {}", my_cheat.cache.client )
    fantasy.log( "dwLocalPlayer: {}", my_cheat.cache.patterns[ "client.dll" ][ "dwLocalPlayerController" ] )
    fantasy.log( "dwLocalPlayerPawn: {}", my_cheat.cache.patterns[ "client.dll" ][ "dwLocalPlayerPawn" ] )
    fantasy.log( "dwEntityList: {}", my_cheat.cache.patterns[ "client.dll" ][ "dwEntityList" ] )
    fantasy.log( "entity_list: {}", my_cheat.cache.entity_list )
end

function my_cheat.on_worker( )

    --[[
    -- we're going to make a simple in crosshair triggerbot script.
    --
    -- 1) get our localplayer's pawn
    -- 2) read C_CSPlayerPawn->m_iIDEntIndex
    -- 3) shoot with some randomization
    --]]
    local local_pawn = my_cheat.cache.client:read(
        MEM_ADDRESS,
        my_cheat.cache.patterns[ "client.dll" ][ "dwLocalPlayerPawn" ]
    )
    if not local_pawn:is_valid( ) then return end

    --[[
    -- check the entity index our crosshair is over
    -- this is usually -1 if someone is staring at a wall or something without a proper entity
    --]]
    local m_iIDEntIndex = local_pawn:read(
        MEM_INT,
        my_cheat.cache.schemas[ "client.dll" ][ "classes" ][ "C_CSPlayerPawn" ][ "fields" ][ "m_iIDEntIndex" ]
    )
    if m_iIDEntIndex == -1 then return end

    --[[
    -- we have the entity index, let's get their pawn as well (if it exists)
    -- it should be listed as an entity as well
    --]]
    local list_entry = my_cheat.cache.entity_list:read(
        MEM_ADDRESS,
        0x8 * ( bit.rshift( m_iIDEntIndex, 9 ) ) + 0x10
    )
    if not list_entry:is_valid( ) then return end

    local entity_pawn = list_entry:read(
        MEM_ADDRESS,
        0x78 * ( bit.band( m_iIDEntIndex, 0x1FF ) )
    )
    if not entity_pawn:is_valid( ) then return end

    --[[
    -- we found an entity. at this point we can start doing validity checks
    -- let's just only check if they're alive right now.
    --
    -- m_lifeState is not a good way to do this because some entities aren't marked as alive for some reason in bot games for example.
    -- sometimes objects will be marked as alive. obviously, this is unpredictable. just check their health.
    --]]
    local m_iHealth = entity_pawn:read(
        MEM_INT,
        my_cheat.cache.schemas[ "client.dll" ][ "classes" ][ "C_BaseEntity" ][ "fields" ][ "m_iHealth" ]
    )
    if m_iHealth <= 0 then return end

    --[[
    -- shoot with some random delay
    -- it would be better if we used input:key to check if a triggerbot key is down
    --]]
    modules.input:click(
        1,
        modules.random:int( 600, 1000 )
    )
end

return my_cheat
```

## battlebitlean.lua
```lua
--[[
    @title
        Battlebit Remastered Lean Spam

    @author
        lu.

    @description
        Battlebit Remastered Lean Spam, makes it harder to hit you.
]]--

local modules = require 'modules'
local battlebitlean = {  
    input = modules.input,  
    jiggle = true, -- Spams lean when shooting (Basically antiaim B)
    jiggle_need_keybind = true, -- Set this to false if you just want it to activate when you fire. When true, you only need to hit the keybind.
    jiggle_keybind = 5, -- https://cherrytree.at/misc/vk.htm
    lean_left = 56, -- 8
    lean_right = 57, -- 9
    timer = 0,
    flip = false,
}

function battlebitlean.on_worker()
    if not battlebitlean.jiggle_need_keybind then
        if battlebitlean.input:is_key_down(1) then
            battlebitlean.timer = battlebitlean.timer + 1
            if battlebitlean.flip == false and battlebitlean.timer <= 9 then
                battlebitlean.input:key(battlebitlean.lean_left, 100)
                battlebitlean.flip = true
            end

            if battlebitlean.timer >= 10 and battlebitlean.flip then
                battlebitlean.input:key(battlebitlean.lean_right, 100)
                battlebitlean.flip = false
            end

            if battlebitlean.timer >= 20 then
                battlebitlean.timer = 0
            end
        else
            battlebitlean.timer = 0
        end
    else
        if battlebitlean.input:is_key_down(battlebitlean.jiggle_keybind) then
            battlebitlean.timer = battlebitlean.timer + 1
            if battlebitlean.flip == false and battlebitlean.timer <= 9 then
                battlebitlean.input:key(battlebitlean.lean_left, 100)
                battlebitlean.flip = true
            end

            if battlebitlean.timer >= 10 and battlebitlean.flip then
                battlebitlean.input:key(battlebitlean.lean_right, 100)
                battlebitlean.flip = false
            end

            if battlebitlean.timer >= 20 then
                battlebitlean.timer = 0
            end
        else
            battlebitlean.timer = 0
        end
    end
end

return battlebitlean
```

## spread_circle.lua
```lua
--[[
    @title
        Spread Circle

    @author
        Moyo

    @description
        draws a circle around the crosshair that visualizes weapon spread
--]]

local modules = require("modules")
local players = require("players")

local spread_circle = {
    enabled = true,
    filled = true,
    follow_recoil = true,
    color_circle = "FF00FFA0",
    color_filled = "FF00FF28",
}

function spread_circle.on_solution_calibrated(info)

    if info.gameid ~= GAME_CS2 then
        fantasy.log("This script only supports CS2. Exiting...")
        return false
    end
end

function spread_circle.on_worker( is_calibrated, game_id )

    -- check if we're calibrated and the script is enabled
    if not is_calibrated or not spread_circle.enabled then return end

    -- get localplayer
    local localplayer = modules.entity_list:get_localplayer( )
    if not localplayer then return end
    localplayer = players.to_player( localplayer )
    if not localplayer:is_alive() then return end

    -- get spread value
    local spread = localplayer:get_spread()
    if spread == nil or spread <= 0 then return end

    -- get camera services and FOV
    local camera_services = localplayer:get_pawn():read(MEM_ADDRESS, modules.source2:get_schema("C_BasePlayerPawn", "m_pCameraServices"))
    if not camera_services then return end
    local fov = camera_services:read(MEM_INT, modules.source2:get_schema("CCSPlayerBase_CameraServices", "m_iFOVStart"))
    if fov == nil then return end

    -- get screen size
    local _, window_width, window_height = fantasy.engine.w2s( nil )

    -- get recoil
    local recoilX, recoilY = 0, 0
    if spread_circle.follow_recoil and localplayer:get_shots_fired() > 1 then
        local aim_punch = localplayer:get_aim_punch()
        recoilX = window_width / 90 * aim_punch.y
        recoilY = window_height / 90 * aim_punch.x
    end

    -- draw spread circle
    local cone_size = (spread * window_height) * 0.7 * (90 / fov)
    if spread_circle.filled then
        modules.kernel:circlef( window_width / 2 - recoilX, window_height / 2 + recoilY, cone_size, color:new( spread_circle.color_filled ) )
    end
    modules.kernel:circle( window_width / 2 - recoilX, window_height / 2 + recoilY, cone_size, color:new( spread_circle.color_circle ) )

end

return spread_circle
```