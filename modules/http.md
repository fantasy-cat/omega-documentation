# http

With any HTTP module request, you can pass the `no_debug` parameter to prevent FC2's console/terminal from showing the outcome. This can be useful for `/luar`.

## ```get```
###Type
`function`

###Parameters
- `string` url
- `table` headers (optional)
- `function` multithread/callback (optional)

###Returns
- `string`

### Example
```lua
local http_test = {}

function http_test.on_loaded()

    -- fetch http module
    local http = fantasy.http()

    -- send http request
    local output = http:get("https://httpbin.org/headers")

    -- output
    fantasy.print( "{}", output )

    -- read result
    fantasy.wait()

end

return http_test
```

### Example (Headers)
```lua
local headers = {}

function headers.on_loaded()

    -- fetch http module
    local http = fantasy.http()

    -- send http request
    local output = http:get(
        "https://httpbin.org/headers",
        {
            "User-Agent: curl/7.87.0",
            "Authorization: ApplesAndBananas",
            "X-Custom-Header: OrangesAndGrapes"
        }
    )

    -- output
    fantasy.print( "{}", output )

    -- read result
    fantasy.wait()

end

return headers
```

### Example (Multithread + Callback)
```lua
local timeout = {}

function timeout.on_loaded()

    -- clock time when script launched
    fantasy.print("time on loaded: {}", os.clock())

    -- http request
    fantasy.http():get(
        "https://httpbin.org/headers",  -- url
        {},                             -- headers
        function( result )              -- multithread + callback/result
            fantasy.print("http output ({}): {}", os.clock(), result )
        end
    )

    -- clock time when on_loaded is done
    fantasy.print("time on finish loaded: {}", os.clock() )

end

return timeout
```

------------

## ```post```
###Type
`function`

###Parameters
- `string` url
- `string` data
- `table` headers (optional)
- `function` multithread/callback (optional)

###Returns
- `string`

------------

## ```escape```
###Type
`function`

###Parameters
- `string` string

###Returns
- `string`

------------

## ```to_file```
###Type
`function`

### Description
The returned `string` contains the content of the file_name/path that was written to. Therefore, this function not only downloads content to a file, but reads the content back to you after.

###Parameters
- `string` url
- `string` file_name/path
- `table` headers (optional)
- `function` multithread/callback (optional)

###Returns
- `string`

------------

## ```open```
###Type
`function`

###Description
Opens a URL in your browser.

###Parameters
- `string` url

------------

## ```new```
###Type
`function`

###Description
Opens a new FC2 HTTP server. This function is useful if you want to bind the current solution's HTTP methods to an IP address. This will allow you to access the server through other devices on the network. Be wary of port usage as if the port is already being used by the host, this function will fail.

###Parameters
- `string` host
- `number` port