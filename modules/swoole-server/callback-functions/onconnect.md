## Events and Callback functions 

### onConnect

This event `connect` happens when the new connection comes. And the worker process will call the callback function registered for the event `connect`.

> In the mode `UDP`, there is only `receive` event and there is no `connect` and `close` event.

#### Example

```php
function onConnect(swoole_server $server, int $fd, int $from_id);
```

- `$fd` the id number of client

- `$from_id` the id number of reactor thread
