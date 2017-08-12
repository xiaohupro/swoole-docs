## Swoole Server

### Methods

#### swoole_server::__construct

Construct a swoole server object:

``` php
<?php

$serv = new swoole_server(string $host, int $port, int $mode = SWOOLE_PROCESS, int $sock_type = SWOOLE_SOCK_TCP);
```
* $host: the ip address of the server
* $port: the port of the server (it needs root privileges if the port is litte than 1024)
* $mode: the running mode of the server:
    * SWOOLE_PROCESS: multiple process mode, the business logic is running in child processes, the default running mode of server
    * SWOOLE_BASE: reactor based mode, the business logic is running in the reactor
* $sock_type: the socket type of the server:
    * SWOOLE_SOCK_TCP: TCP
    * SWOOLE_SOCK_TCP6: TCP IPv6
    * SWOOLE_SOCK_UDP: UDP
    * SWOOLE_SOCK_UDP6: UDP IPv6
    * SWOOLE_UNIX_DGRAM: Unix socket dgram
    * SWOOLE_UNIX_STREAM: Unix socket stream
* Enable SSL: `$sock_type | SWOOLE_SSL`. To enable ssl, it must set [the configuration about ssl](/modules/swoole-server/configuration.md).

Example:

##### Listen on a random port:

``` php
<?php
$http = new swoole_http_server("0.0.0.0");

$http->on('request', function ($request, $response) {
    $response->header("Content-Type", "text/html; charset=utf-8");
    $response->end("<h1>Hello Swoole. #".rand(1000, 9999)."</h1>");
});

$http->start();
```
##### Listen on a port defined in systemd

*swoole.socket*
``` bash
[Unit]
Description=Swoole Socket

[Socket]
ListenStream=9501
Accept=false
[Install]
WantedBy = sockets.target
```

*swoole.service*
``` bash
[Service]
Type=forking
PIDFile=/var/run/swoole.pid
ExecStart=/usr/bin/php /var/www/swoole/server.php
ExecStop=/bin/kill $MAINPID
ExecReload=/bin/kill -USR1 $MAINPID

[Install]
WantedBy = multi-user.target
```

*server.php*
``` php
$http = new swoole_http_server("systemd");

$http->set([
    'daemonize' => true,
    'pid_file' => '/var/run/swoole.pid',
]);

$http->on('request', function ($request, $response) {
    $response->header("Content-Type", "text/html; charset=utf-8");
    $response->end("<h1>Hello Swoole. #".rand(1000, 9999)."</h1>");
});

$http->start();
```

*Start the systemd service*

``` bash
sudo systemctl enable swoole.socket
sudo systemctl start swoole.socket
sudo systemctl start swoole.service
```

#### function swoole_server->set(array $setting);

Set the settings of the swoole server:

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

> Have to be set before swoole_server->start()

Other settings:

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

#### bool swoole_server->on(string $event, mixed $callback);

Register callback function for the events:

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

#### function swoole_server->addListener(string $host, int $port, $type = SWOOLE_SOCK_TCP);

Add more listening IP or port for the server.

Example:

``` php
<?php
$server->addlistener("127.0.0.1", 9502, SWOOLE_SOCK_TCP);
$server->addlistener("192.168.1.100", 9503, SWOOLE_SOCK_TCP);
$server->addlistener("0.0.0.0", 9504, SWOOLE_SOCK_UDP);
//UnixSocket Stream
$server->addlistener("/var/run/myserv.sock", 0, SWOOLE_UNIX_STREAM);
//TCP + SSL
$server->addlistener("127.0.0.1", 9502, SWOOLE_SOCK_TCP | SWOOLE_SSL); 
//Listen on a random port
$port = $server->addListener("0.0.0.0", 0, SWOOLE_SOCK_TCP);
echo $port->port;
```

#### bool swoole_server->addProcess(swoole_process $process);

Add a user defined child process to the server. The process can be used as monitoring or other tasks.

Example:

``` php
<?php
$server = new swoole_server('127.0.0.1', 9501);

$process = new swoole_process(function($process) use ($server) {
    while (true) {
        $msg = $process->read();
        foreach($server->connections as $conn) {
            $server->send($conn, $msg);
        }
    }
});

$server->addProcess($process);

$server->on('receive', function ($serv, $fd, $from_id, $data) use ($process) {
    // send the data received to all the child processes
    $process->write($data);
});

$server->start();
```

#### bool swoole_server->listen(string $host, int $port, int $type);

Alias of bool swoole_server->addlistener(string $host, int $port, int $type);

#### bool swoole_server->start()

Start the swoole server, it will create worker_num + 2 processes by default:

* main process: running multiple threads reactor, receive new connections and assign connections to worker processes
* manager process: managing the worker processes
* worker_num * child processes: process the data and business logics

#### bool swoole_server->reload(bool $only_reload_taskworkrer = false)

Gracefully restart all the worker processes and reload the PHP files.

##### Restart all the worker processes by signal

``` bash
kill -USR1 MASTER_PID
```

##### Only restart the task processes by signal

``` bash
kill -USR2 MASTER_PID
```

##### Get all the files loaded before the worker started

``` php
<?php
$server->on('WorkerStart', function($serv, $workerId) {
    var_dump(get_included_files());
});
```

##### When using APC/OpCache

* *stat* in APC/OpCache has to be enabled for code reload
* Refresh OpCache with apc_clear_cache() or opcache_reset() if necessary

#### function swoole_server->stop($worker_id);

Stop current worker process or worker process by ID, this will emit 'WorkerStop' event and trigger the WorkerStop callback function.

#### function swoole_server->kill($worker_id);

Kill and terminate worker process by ID.

#### void swoole_server->shutdown();

Shutdown the master server process, this function can be called in worker processes.

##### Shutdown server by system signal *SIGTERM*

``` bash
kill -15 MASTER_PID
```

#### $server->tick(1000, function() use ($server, $fd))

Trigger a timer tick by interval. Alias of function *swoole_timer_tick()*.

Example:

``` php
<?php
function onReceive($server, $fd, $from_id, $data) {
    $server->tick(1000, function() use ($server, $fd) {
        $server->send($fd, "hello world");
    });
}
```

#### swoole_server->after(int $after_time_ms, mixed $callback_function);

Trigger a one time tick in the future. Alias of function *swoole_timer_after()*.

#### function swoole_server->defer(callable $callback);

Delay execution of the callback function at the end of current *EventLoop*. Alias of function *swoole_event_defer()*.

Example:

``` php
<?php
function query($server, $db) {
    $server->defer(function() use ($db) {
        $db->close();
    });
}
```

#### $server->clearTimer($id);

Cancel the timer tick or one time tick. Alias of function *swoole_timer_clear*.

Example:

``` php
<?php
$timer_id = $server->tick(1000, function ($id) use ($server) {
    $server->clearTimer($id);
});
```

#### bool swoole_server->close(int $fd, bool $reset = false);

Close the connection to the remote TCP socket and emit *Close* event.

#### bool swoole_server->send(int $fd, string $data, int $reactorThreadId = 0);

Send data to the remote TCP socket.

> The max TCP data size is 2MB, and the max UDP data size is 64KB.

#### bool swoole_server->sendfile(int $fd, string $filename, int $offset =0, int $length = 0);

Send large size data or files to the remote TCP socket. A wrapper of the *sendfile* system call.

Example:

``` php
<?php
$server->sendfile($fd, __DIR__.'/test.jpg');
```

#### bool swoole_server->sendto(string $ip, int $port, string $data, int $server_socket = -1);

Send data to the remote UDP address.

Example:

```php
<?php
$server->sendto('220.181.57.216', 9502, "hello world");
$server->sendto('2600:3c00::f03c:91ff:fe73:e98f', 9501, "hello world");
```

#### bool swoole_server->sendwait(int $fd, string $send_data);

Send data to the remote socket in the blocking way.

> Only available in SWOOLE_BASE mode.

#### bool swoole_server->sendMessage(string $message, int $dst_worker_id);

Send message to worker processes by ID.

Exmaple:

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

#### function swoole_server->exist(int $fd);

Check whether the (TCP) file description is existed.

#### function swoole_server->pause(int $fd);

Pause the data receiving.

> Only available in SWOOLE_BASE mode.

#### function swoole_server->resume(int $fd);

Resume the data receiving.

> Only available in SWOOLE_BASE mode.

#### function swoole_server->connection_info(int $fd, int $from_id, bool $ignore_close = false)

Get the connection info, alias of function *swoole_server->getClientInfo()*.

Example:

``` php
<?php
$fdinfo = $serv->connection_info($fd);
var_dump($fdinfo);
array(5) {
  ["from_id"]=>
  int(3)
  ["server_fd"]=>
  int(14)
  ["server_port"]=>
  int(9501)
  ["remote_port"]=>
  int(19889)
  ["remote_ip"]=>
  string(9) "127.0.0.1"
  ["connect_time"]=>
  int(1390212495)
  ["last_time"]=>
  int(1390212760)
}

$udp_client = $serv->connection_info($fd, $from_id);
var_dump($udp_client);
```

#### swoole_server::connection_list(int $start_fd = 0, int $pagesize = 10);

Get the list of all the TCP connections.

Example:

``` php
<?php
$start_fd = 0;
while(true)
{
    $conn_list = $serv->connection_list($start_fd, 10);
    if($conn_list===false or count($conn_list) === 0)
    {
        echo "finish\n";
        break;
    }
    $start_fd = end($conn_list);
    var_dump($conn_list);
    foreach($conn_list as $fd)
    {
        $serv->send($fd, "broadcast");
    }
}
```

#### bool swoole_server::bind(int $fd, int $uid)

Bind the fd with system user UID.

#### array swoole_server->stats();

Get the TCP connections stats of the current server.

Example result:

``` php
<?php
array (
  'start_time' => 1409831644,
  'connection_num' => 1,
  'accept_count' => 1,
  'close_count' => 0,
);
array (
  'task_queue_num' => 10,
  'task_queue_bytes' => 65536,
);
```

#### int swoole_server::task(mixed $data, int $dst_worker_id = -1);

Send data to the task worker processes.

Example:

``` php
<?php
int swoole_server::task(mixed $data, int $dst_worker_id = -1) 
$task_id = $server->task("some data");

$server->task("taskcallback", -1, function (swoole_server $serv, $task_id, $data) {
    echo "Task Callback: ";
    var_dump($task_id, $data);
});
```

#### string $result = swoole_server->taskwait(mixed $task_data, float $timeout = 0.5, int $dst_worker_id = -1);

Send data to the task worker processes after the delayed period of time.

#### function swoole_server->taskWaitMulti(array $tasks, double $timeout);

Execute multiple tasks concurrently, example:

``` php
<?php
$tasks[] = mt_rand(1000, 9999); 
$tasks[] = mt_rand(1000, 9999); 
$tasks[] = mt_rand(1000, 9999); 
var_dump($tasks);

$results = $serv->taskWaitMulti($tasks, 10.0);

if (!isset($results[0])) {
    echo "Task 1: timeout.\n";
}
if (isset($results[1])) {
    echo "Task 2: {$results[1]}\n";
}
if (isset($results[2])) {
    echo "Task 3: {$results[2]}\n";
}
```

#### function swoole_server->finish("response");

Used in task process for sending result to the worker process when the task is finished.

#### array swoole_server::heartbeat(bool $if_close_connection = true);

Check status of all the connections of the server. Optionally close the idle and timeout connections.

#### function swoole_server->getLastError()

Get the error code of the most recent error.

Error codes:
* 1001: The connection has been closed by the server.
* 1002: The connection has been closed by the client side.
* 1003: The connection is closing.
* 1004: The connection is closed.
* 1005: Error $fd.
* 1007: Received data after connection has been closed.
* 1008: The send buffer is full.

#### $server->getSocket();

Get socket and update the options of the socket.

Example:

``` php
<?php
$socket = $server->getSocket();
if (!socket_set_option($socket, SOL_SOCKET, SO_REUSEADDR, 1)) {
    echo 'Unable to set option on socket: '. socket_strerror(socket_last_error()) . PHP_EOL;
}
```

Multi cast example:

``` php
<?php
$server = new swoole_server('0.0.0.0', 9905, SWOOLE_BASE, SWOOLE_SOCK_UDP);
$server->set(['worker_num' => 1]);
$socket = $server->getSocket();

$ret = socket_set_option(
    $socket,
    IPPROTO_IP,
    MCAST_JOIN_GROUP,
    array('group' => '10.0.0.5', 'interface' => 'eth0')
);

if ($ret === false)
{
    throw new RuntimeException('Unable to join the multicast group');
}

$server->on('Packet', function (swoole_server $serv, $data, $addr)
{
    $serv->sendto($addr['address'], $addr['port'], "Swoole: $data");
    var_dump( $addr, strlen($data));
});

$server->start();
```
