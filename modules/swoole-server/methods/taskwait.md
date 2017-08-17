## Method

### swoole_server->taskwait

#### Prototype

```php
string/bool swoole_server->taskwait(mixed $task_data, float $timeout = 0.5, int $dst_worker_id = -1)
```

#### Illustration

The `swoole_server->taskwait` is similar to `swoole_server->task`. The two methods both send task data to the task worker pool to execute, but the former is blocking.

This method 

#### Parameter

* `$data`	the data which is to send to the task worker, its type could any type except fot resource
* `$dst_worker_id` the id number of task worker. If this parameter hasn't been passed, the swoole server would select a random and unoccupied task worker process.
* `$callback` the callback function be called when the task has been finished. If this parameter has been passed, there is no need to register the callback function of the event of `onFinish`

#### Return

If the call of this method succeeds, the return is the task id which identifies the task
If the call of this method fails, the return is false

#### Example

``` php
<?php
$task_id = $server->task("some data");

$server->task("taskcallback", -1, function (swoole_server $serv, $task_id, $data) {
    echo "Task Callback: ";
    var_dump($task_id, $data);
});
```
