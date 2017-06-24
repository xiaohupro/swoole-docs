# Swoole server

Swoole server component enable developers to write TCP, UDP, UnixSocket servers. It supports IPv4, IPv6, One Way and Two Way SSL and TLS Encryption**. **Developers do not have to know the internal implementations , only have to write business logic in the callback functions.

## Initialize the server

``` php
$serv = new swoole_server("127.0.0.1", 9501, SWOOLE_BASE, SWOOLE_SOCK_TCP);
```

## Runtime paramaters

``` php
$serv->set(array(
    'worker_num' => 4, // The number of worker processes
    'daemonize' => true, // Whether start as a daemon process
    'backlog' => 128, // TCP backlog connection number
));
```

## Callback functions

``` php
$serv->on('Connect', 'my_onConnect');
$serv->on('Receive', 'my_onReceive');
$serv->on('Close', 'my_onClose');
```

## Start the server

``` php
$serv->start();
```

## Internal variables

``` php
$serv->manager_pid; // PID of manager process, send SIGUSR1 to this process to reload the application
$serv->master_pid;  // PID of master process, send SIGTERM signal to this process to shutdown the server
$serv->connections; // The connections established
```

## How it works



