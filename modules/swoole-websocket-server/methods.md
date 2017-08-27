# Swoole WebSocket server

## Method

The `swoole_websocket_server` class inherits from the class `swoole_server`. It has also its own method.

### swoole_websocket_server->push

#### Illustration

This method is to push the message to the client. The max length of message is 2M.

#### Prototype

```php
bool swoole_websocket_server->push(int $fd, string $data, int $opcode = 1, bool $finish = true);
```
- `$fd` the id number of client. If the client isn't websocket client, the push will fail.

- `$data` the message to send

- `$opcode` the format of message to send. The default is text. If you want to send binary data, the value of this parameter should be `WEBSOCKET_OPCODE_BINARY`

- If the push of message succeeds, the return is `true` otherwise `false`
