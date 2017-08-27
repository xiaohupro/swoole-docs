# Swoole WebSocket server

## Events and Callback Functions

### onMessage

The event `message` happens when the swoole websocket server receives the data frame from the client.

#### Example

```php
function onMessage(swoole_server $server, swoole_websocket_frame $frame)
```

- `$frame` the object of class `swoole_websocket_frame`. It contains the infomation from the client

> For swoole websocket server, it must set the callback function for the event `message`

> The `ping` frame from the client will not trigger the event `message` and the swoole websocket server will respond `pong` automatically.

#### swoole_websocket_frame

The class `swoole_websocket_frame` has four properties:

- `$frame->fd` the id number of client

- `$frame->data` the data from the client. It can be text or binary data which can be distinguished by the value of `$frame->opcode`.

- `$frame->opcode` the opcode type of websocket

- `$frame->finish` if the data frame is complete.

#### OpCode and Data type

- WEBSOCKET_OPCODE_TEXT = 0x1, text

- WEBSOCKET_OPCODE_BINARY = 0x2, binary data
