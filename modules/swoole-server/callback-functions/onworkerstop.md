## Events and Callback functions 

### onWorkerStop

This event `workerstop` happens when the worker process stops.

In the callback function registered for the event `workerstop`, you can retrieve or release the resource for the worker process which stops.

> The abnormal stop of worker process will not trigger the event `workerstop`, for example, fatal error, core dump

#### Example

```php
function onWorkerStop(swoole_server $server, int $worker_id);
```
