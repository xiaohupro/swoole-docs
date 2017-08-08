## Events

* start
* shutdown
* managerstart
* managerstop
* workerstart
* workerstop
* connect
* receive
* packet
* close
* bufferempty
* bufferfull
* task
* timer
* finish
* pipemessage
* workererror

Example of writing callback functions, or register event callback functions:

``` php
<?php
$server = new swoole_server("127.0.0.1", 9501, SWOOLE_BASE, SWOOLE_SOCK_TCP);
$server->on('WorkerStart', function($serv, $workerId) {
    var_dump(get_included_files());
});
```
