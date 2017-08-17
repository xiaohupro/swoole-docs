## Method

### swoole_server->task

#### Prototype

```php
int swoole_server->task(mixed $data, int $dst_worker_id = -1, callable $callback = NULL)
```

#### Illustration

Send data to the task worker processes.

> To call this method, it needs to set [the configuration of task_worker_num](/modules/swoole-server/configuration/task_worker_num.md) and the callback function of [onTask](/modules/swoole-server/callback-functions/ontask.md) and [onFinish](/modules/swoole-server/callback-functions/onfinish.md)
> This method is non-blocking and return immediately after sending the task data to the pool of task worker.

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
