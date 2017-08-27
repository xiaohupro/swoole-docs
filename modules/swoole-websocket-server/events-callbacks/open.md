# Swoole WebSocket server

## Events and Callback Functions

### onOpen

The event `open` happens when the websocket server and client has created the connection and finished the handshake. And the callback function registered for event `open` will be called.

#### Example

```php
function onOpen(swoole_websocket_server $svr, swoole_http_request $req)
```

- `$req` the object of http request, it contains the information of client

> In the callback function for event `open`, you can push message to client and close the connection.

> The callback function for event `open` is optional.
