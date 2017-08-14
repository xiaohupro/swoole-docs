## Method

### swoole_server->set 

#### Prototype

```php
void swoole_server->set(array $setting)
```

#### Illustration

Set the runtime settings of the swoole server. The settings can be accessed by `$server->setting` when the swoole server has started.

#### Parameter

* `$setting` the array of runtime settings

Setting example:

* max_conn => 10000: the max tcp connection number of the server
* daemonize => 1: enable the daemon mode the server process
* reactor_num => 2: set the number of system poll threads, the default setting is the number of CPU cores
* worker_num => 4: set the number of worker processes 
* max_request => 2000: the number of requests processed by the worker process before been recycled
* backlog => 128: TCP backlog number, the max number of connections waiting for acception
* open_cpu_affinity => 1: enable CPU affinity
* open_tcp_nodelay => 1: enable TCP_NoDelay
* tcp_defer_accept => 5: delay a period of time for the new connection before been accepted
* log_file => '/data/log/swoole.log': set the error logs location of the server
* open_eof_check => true: enable buffer for the data receiving
* package_eof => "\r\n\r\n": set EOF of the packages
* heartbeat_check_interval => 30: set the interval of health checking for the TCP connections
* heartbeat_idle_time => 60: set the max idle time before the idel connection been closed
* dispatch_mode = 1: dispatch mode for child processes:
    * 1: round robin assignment
    * 2: assignment by mod
    * 3: preemptive assignment

> Check [the full list of settings](/modules/swoole-server/configuratio.md)

#### Return

void

#### Example

``` php
<?php
$server->set(array(
    'reactor_num' => 2, //reactor thread num
    'worker_num' => 4,    //worker process num
    'backlog' => 128,   //listen backlog
    'max_request' => 50,
    'dispatch_mode' => 1,
));
```
