## Method

### swoole_server->getLastError()

#### Prototype

```php
int swoole_server->getLastError()
```

#### Illustration

Get the error code of the most recent error.

#### Parameter

void

#### Return

the error code

Error codes:
* 1001: The connection has been closed by the server.
* 1002: The connection has been closed by the client side.
* 1003: The connection is closing.
* 1004: The connection is closed.
* 1005: Error $fd.
* 1007: Received data after connection has been closed.
* 1008: The send buffer is full.

#### Example
