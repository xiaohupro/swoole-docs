## Events and Callback functions 

### onClose

The event `close` happens when the TCP connection between the client and the server is closed.

The worker process will call the callback function registered for the event `close`.

#### Example

```php
function onClose(swoole_server $server, int $fd, int $reactorId);
```

- `$server` the swoole server object

- `$fd` the id number of client

- `$reactorId` the id number of reactor thread, when the `$reactorId` < 0, the connection is closed by server.
