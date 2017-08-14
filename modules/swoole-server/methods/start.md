## Method

### swoole_server->start

#### Prototype

```php
bool swoole_server->start()
```

#### Illustration

Start the swoole server, it will create worker_num + 2 processes by default:

* main process: running multiple threads reactor, receive new connections and assign connections to worker processes
* manager process: managing the worker processes
* worker_num * child processes: process the data and business logics

#### Parameter

void

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
    $server->send($fd, "Echo to #{$fd}: \n".$data);
    $server->close($fd);
});
$server->on('close', function ($server, $fd) {
    echo "Connection closed: #{$fd}.\n";
});
$server->start();
```
