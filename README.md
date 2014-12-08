# lua-http
Lua HTTP client cosocket based on [OpenResty](http://openresty.org/) / [ngx_lua](https://github.com/chaoslawful/lua-nginx-module).

# Features
* Support HTTP 1.1
* Support chunked encoding
* Keepalive

# Useage

   local h = s2http:new( ip, port, timeout )

   h:request( uri, {method='GET', headers={}, body=''} )

   status = h.status

   headers = h.headers

   buf = h:read_body( size )

or

   local h = s2http:new( ip, port, timeout )

   h:send_request( uri, {method='GET', headers={}, body=''} )

   h:send_body( body )

   h:finish_request()

   status = h.status

   headers = h.headers

   buf = h:read_body( size )

# Interfaces

## new

`syntax: http = http:new( ip, port?, timeout? )`

Creates the http object.

It should be instantiated passing it ip and optional port number. If no port
number is passed, the default HTTP port (80) is used. If no timeout, then
defalut timeout is 60s

## request
` syntax: err_code, err_msg = http:request( uri, opts? )`

Send a request to the server by specified uri. If the opts argument is present,
It should be a table, The opts table accepts the following items:

* `method`: The HTTP request method. Defaults is `GET`.
* `headers`: A table of request headers. Accepts a Lua table.
* `body`: The request body as a string.

In case of success, this method returns nil, nil and http object contains status, headers;

otherwise, it returns err_code and a string describing the error.

## send_request
` syntax: err_code, err_msg = http:send_request( uri, opts? )`

As the above, `requset` method, but this method does not contains http
response(eg: status, headers), you can call `finish_request` later.

In case of failure, it returns err_code and a string describing the error.

## send_body
` syntax: bytes, err_code, err_msg = http:send_body( body )`

Send data to the server

In case of success, this method returns bytes, nil, nil, the return value bytes is the length of send body;

otherwise, it returns err_code and a string describing the error.

## finish_request
` syntax: err_code, err_msg = http:finish_requst()`

Send the request to the server really,

In case of success, this method returns nil, nil, the http status and headers seted in http object,
suce as, http.status, http.headers

## read_body
` syntax: buf, err_code, err_msg = http:read_body( size )`

Read the http response body of the specified size

## set_timeout
` syntax: err_code, err_msg = http:set_timeout( time )`

Set the timeout value in milliseconds for http connection

## set_keepalive
` syntax: err_code, err_msg = http:set_keepalive( timeout, size )`

The same as [ngx_lua setkeeeplive](http://wiki.nginx.org/HttpLuaModule#tcpsock:setkeepalive)

## close
` syntax: http:close()`

Close the http connection to the server
