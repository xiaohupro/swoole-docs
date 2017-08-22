## Events and Callback functions 

### onFinish

When the task finished, the task result would be sent to worker process and trigger the event `finish`.

#### Example

```php
void onFinish(swoole_server $serv, int $task_id, string $data)
```

- `$serv` the swoole server object

- `$task_id` the id number of task

- `$data` the result of task
