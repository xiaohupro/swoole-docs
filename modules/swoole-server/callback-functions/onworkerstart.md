## Events and Callback functions 

### onWorkerStart

The event `workerstart` happens when the worker process or task worker process starts.

According to the value of `$worker_id`, if `$worker_id>= $serv->setting['worker_num'] `, the worker is a task worker process otherwise it is a worker process.

> There is no relation between `worker_id` and pid of process.

#### Example

```php
function onWorkerStart(swoole_server $server, int $worker_id)
```

#### Usage 

```php
$serv->on('WorkerStart', function ($serv, $worker_id){
    global $argv;
    if($worker_id >= $serv->setting['worker_num']) {
        swoole_set_process_name("php {$argv[0]} task worker");
    } else {
        swoole_set_process_name("php {$argv[0]} event worker");
    }
});
```
