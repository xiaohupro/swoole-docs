## Method

### swoole_server->close

#### Prototype

```php
bool swoole_server->close(int $fd, bool $reset = false)
```

#### Illustration

Close the connection to the remote TCP socket and emit *Close* event.

#### Parameter

* `$fd`	the id of connection between the server and the client
* `$reset` if close the connection forcibly and loose the data of this connection

#### Return

the result of close the connection

#### Example
