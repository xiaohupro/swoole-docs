## Events and Callback functions 

### onTask

The event `task` happens when the worker process send a task data to task worker processed pool.

The task worker process which has received the task data will call the callback function registered for the event `task`.

When the task worker process is processing the task, its status is busy and changes to idle after finishing the task.

#### Example

```php
function onTask(swoole_server $serv, int $task_id, int $src_worker_id, mixed $data);
```

- `$serv` the swoole server object

- `$task_id` the id number of task, the combination of `$task_id` and `$src_worker_id` is an unique identification for task

- `$data` the task data


#### Return task result to worker process

In the callback function registered for event `task`, the return of this function is the result of task and will be sent to the worker process which sent the task. You can also return the result of task by calling `swoole_server->finish()`.

When the worker process has received the task result, the event `finish` would be triggered and call the function registered for event `finish` in the worker process.
