## Method

### swoole_server->sendMessage

#### Prototype

```php
bool swoole_server->sendMessage(string $message, int $dst_worker_id)
```

#### Illustration

Send message to worker processes by ID. This message will trigger the event of `pipe message` and the process which has received this message would call the callback function registered for `pipe message`.

> There is no length limit for the message, but the server will use the temporary file in the memory if the length of file is bigger than 8K
> In the task worker process, `sendMessage` is blocking
> In the worker process, `sendMessage` is async.

#### Parameter

* `$message`	the string of message to send
* `$dst_worker_id` the integer of worker process which is between 0 and (worker_num + task_worker_num - 1)

#### Return

the result of send message to worker

#### Example

``` php
<?php
$serv = new swoole_server("0.0.0.0", 9501);
$serv->set(array(
    'worker_num' => 2,
    'task_worker_num' => 2,
));
$serv->on('pipeMessage', function($serv, $src_worker_id, $data) {
    echo "#{$serv->worker_id} message from #$src_worker_id: $data\n";
});
$serv->on('task', function ($serv, $task_id, $from_id, $data){
    var_dump($task_id, $from_id, $data);
});
$serv->on('finish', function ($serv, $fd, $from_id){

});
$serv->on('receive', function (swoole_server $serv, $fd, $from_id, $data) {
    if (trim($data) == 'task')
    {
        $serv->task("async task coming");
    }
    else
    {
        $worker_id = 1 - $serv->worker_id;
        $serv->sendMessage("hello task process", $worker_id);
    }
});

$serv->start();
```
