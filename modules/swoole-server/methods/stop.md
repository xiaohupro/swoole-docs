## Method

### swoole_server->stop

#### Prototype

```php
void swoole_server->stop($worker_id = -1);
```

#### Illustration

Stop current worker process or worker process by ID, this will emit 'WorkerStop' event and trigger the WorkerStop callback function.

- Use the method to replace the function `exit/die` to end the worker process

#### Parameter

* $worker_id : the id of worker process

#### Return

the result if the swoole server starts successfully 

#### Example

``` php
<?php
$server = new swoole_server("127.0.0.1", 9501);
$server->on('connect', function ($server, $fd){
    echo "New connection established: #{$fd}.\n";
});
$server->on('receive', function ($server, $fd, $from_id, $data) {
    if(trim($data) == "stop")
    {
        $server->stop();
    }
    else
    {
        $server->send($fd, "Echo to #{$fd}: \n".$data);
        $server->close($fd);
    }
});

$server->on('WorkerStop', function($server, $worker_id){
    echo $worker_id . " stop\n";
});

$server->on('close', function ($server, $fd) {
    echo "Connection closed: #{$fd}.\n";
});
$server->start();
```
