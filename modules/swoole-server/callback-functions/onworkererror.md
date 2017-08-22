## Events and Callback functions 

### onWorkerError

When there is error or exception in the worker process or task worker process, the event `workererror` happens in the manager process.

The callback function registered for event `workererror` is called in manager process.

#### Example

```php
void onWorkerError(swoole_server $serv, int $worker_id, int $worker_pid, int $exit_code, int $signal);
```

- `$worker_id` the id number of worker

- `$worker_pid` the pid of worker process

- `$exit_code` the exit code of worker process

- `$signal` the exit signal of worker process
