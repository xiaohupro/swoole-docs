## Method

### swoole_server->send

#### Prototype

```php
bool swoole_server->send(int $fd, string $data, int $extraData = 0)
```

#### Illustration

Send data to the remote TCP socket.

* The max TCP data size is 2MB. This limit can be changed by configuring [the configuration of buffer_output_size](/modules/swoole-server/configuration/buffer_output_size.md)
* The max UDP data size is 64KB.
* If the swoole server is type of UDP, `$fd` keeps the ip address of client and `$extraData` keeps the `server_fd` and `port`

#### Parameter

* `$fd`	the id number of client
* `$data` the function that triggered after with a fixed time delay
* `$extraData` the extra data of sending data 

#### Return

the result of send data to the client

If the result is false, you can call the method `$server->getLastError()` to get the error code.

#### Example
