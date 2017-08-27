# Swoole WebSocket server

## Events and Callback Functions

### onHandShake

This event happens when the websocket connection start the handshake process. The `swoole_websocket_server` has built-in callback function registered for event `handshake`. But you can also choose to custom your callback function for event `handshake`.

#### Example

```php
function onHandShake(swoole_http_request $request, swoole_http_response $response)
```

