## Events and Callback functions 

### onPipeMessage

When the worker process or task worker process receives the message sent by `sendMessage`, the event `pipeMessage` happens. 

The callback function registered for event `pipeMessage` will be called.

#### Example

```php
void onPipeMessage(swoole_server $server, int $from_worker_id, string $message);
```

- `$from_worker_id` the id number of worker when the message from

- `$message` the message
