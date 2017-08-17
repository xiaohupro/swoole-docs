## Method

### swoole_server->taskwait

#### Prototype

```php
string/bool swoole_server->taskwait(mixed $task_data, float $timeout = 0.5, int $dst_worker_id = -1)
```

#### Illustration

The `swoole_server->taskwait` is similar to `swoole_server->task`. The two methods both send task data to the task worker pool to execute, but the former is blocking.

#### Parameter

* `$task_data`	the data which is to send to the task worker, its type could any type except fot resource
* `$timeout`    the time of timeout 
* `$dst_worker_id` the id number of task worker. If this parameter hasn't been passed, the swoole server would select a random and unoccupied task worker process.

#### Return

If the call of this method succeeds, the return is the result of task
If the execution of this method exceeds the time of timeout, the return is false

#### Example
