# lua-http
Lua HTTP client cosocket based on [OpenResty](http://openresty.org/) / [ngx_lua](https://github.com/chaoslawful/lua-nginx-module).

# Features
* Support HTTP 1.1
* Support chunked encoding
* Keepalive

# Interfaces

## new

`syntax: http = http:new( ip, port?, timeout? )`

Creates the http object.

It should be instantiated passing it ip and optional port number. If no port
number is passed, the default HTTP port (80) is used. If no timeout, then
defalut timeout is 60s

## request
` syntax err_code, err_msg = http:request( uri, opts? )`

## send_request
` syntax err_code, err_msg = http:send_request( uri, opts? )`

## send_body
` syntax bytes, err_code, err_msg = http:send_body( body )`

## finish_request
` syntax err_code, err_msg = http:finish_requst()`

## read_bodyt
` syntax buf, err_code, err_msg = http:read_body( size )`

## set_timeout
` syntax err_code, err_msg = http:set_timeout( time )`

## set_keepalive
` syntax err_code, err_msg = http:set_keepalive( timeout, size )`

## close
` syntax http:close()`
