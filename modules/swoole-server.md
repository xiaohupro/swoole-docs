# Swoole server

Swoole server component enable developers to write TCP, UDP, UnixSocket servers. It supports IPv4, IPv6, One Way and Two Way SSL and TLS Encryption**. **Developers do not have to know the internal implementations , only have to write business logic in the callback functions.

### Initialize the server

``` php
$server = new swoole_server("127.0.0.1", 9501, SWOOLE_BASE, SWOOLE_SOCK_TCP);
```

### Runtime paramaters

``` php
<?php
$server->set(array(
    'worker_num' => 4, // The number of worker processes
    'daemonize' => true, // Whether start as a daemon process
    'backlog' => 128, // TCP backlog connection number
));
```

### Callback functions

``` php
<?php
$server->on('Connect', 'my_onConnect');
$server->on('Receive', 'my_onReceive');
$server->on('Close', 'my_onClose');
```

### Start the server

``` php
<?php
$server->start();
```

### Attributes

``` php
<?php
$server->manager_pid; // PID of manager process, send SIGUSR1 to this process to reload the application
$server->master_pid;  // PID of master process, send SIGTERM signal to this process to shutdown the server
$server->connections; // The connections established
```

### How it works

### Example

### Methods

#### swoole_server::__construct

Construct a swoole server object:

``` php
<?php

$serv = new swoole_server(string $host, int $port, int $mode = SWOOLE_PROCESS, int $sock_type = SWOOLE_SOCK_TCP);
```
* $host: the ip address of the server
* $port: the port of the server
* $mode: the running mode of the server:
    * SWOOLE_PROCESS: multiple process mode, the business logic is running in child processes
    * SWOOLE_BASE: reactor based mode, the business logic is running in the reactor
* $sock_type: the socket type of the server:
    * SWOOLE_SOCK_TCP: TCP
    * SWOOLE_SOCK_TCP6: TCP IPv6
    * SWOOLE_SOCK_UDP: UDP
    * SWOOLE_SOCK_UDP6: UDP IPv6
    * SWOOLE_UNIX_DGRAM: Unix socket dgram
    * SWOOLE_UNIX_STREAM: Unix socket stream
* Enable SSL: $sock_type | SWOOLE_SSL

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
    echo "Client:Connect.\n";
});
$server->on('receive', function ($server, $fd, $from_id, $data) {
    $server->send($fd, 'Swoole: '.$data);
    $server->close($fd);
});
$server->on('close', function ($server, $fd) {
    echo "Client: Close.\n";
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

Restart all the worker processes.

#### function swoole_server->stop();

#### void swoole_server->shutdown();

#### $server->tick(1000, function() use ($server, $fd))

#### swoole_server->after(int $after_time_ms, mixed $callback_function);

#### function swoole_server->defer(callable $callback);

#### $server->clearTimer($id);

#### bool swoole_server->close(int $fd, bool $reset = false);

#### bool swoole_server->send(int $fd, string $data, int $reactorThreadId = 0);

#### bool swoole_server->sendfile(int $fd, string $filename, int $offset =0, int $length = 0);

#### bool swoole_server->sendto(string $ip, int $port, string $data, int $server_socket = -1);

#### bool swoole_server->sendwait(int $fd, string $send_data);

#### bool swoole_server->sendMessage(string $message, int $dst_worker_id);

#### function swoole_server->exist(int $fd)

#### function swoole_server->pause(int $fd);

#### function swoole_server->resume(int $fd);

#### function swoole_server->connection_info(int $fd, int $from_id, bool $ignore_close = false)

#### swoole_server::connection_list(int $start_fd = 0, int $pagesize = 10);

#### bool swoole_server::bind(int $fd, int $uid)

#### array swoole_server->stats();

#### int swoole_server::task(mixed $data, int $dst_worker_id = -1) 

#### string $result = swoole_server->taskwait(mixed $task_data, float $timeout = 0.5, int $dst_worker_id = -1);

#### array swoole_server->taskWaitMulti(array $tasks, double $timeout);

#### $swoole_server->finish("response");

#### array swoole_server::heartbeat(bool $if_close_connection = true);

#### function swoole_server->getLastError()

#### $socket = $server->getSocket();






