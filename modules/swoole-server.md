## Swoole server

Swoole server component enable developers to write TCP, UDP, UnixSocket servers. It supports IPv4, IPv6, One Way and Two Way SSL and TLS Encryption**. **Developers do not have to know the internal implementations , only have to write business logic in the callback functions.

## Initialize the server

`$serv = new swoole_server("127.0.0.1", 9501, SWOOLE_BASE, SWOOLE_SOCK_TCP);`

## Runtime paramaters

`$serv->set(array(`

`'worker_num' => 4,`

`'daemonize' => true,`

`'backlog' => 128,`

`));`

## Callback functions

`$serv->on('Connect', 'my_onConnect');`

`$serv->on('Receive', 'my_onReceive');`

`$serv->on('Close', 'my_onClose');`

## Start the server

`$serv->start();`

## Internal variables

`$serv->manager_pid; // PID of manager process, send SIGUSR1 to this process to reload the application`

`$serv->master_pid;  // PID of master process, send SIGTERM signal to this process to shutdown the server`

`$serv->connections; // The connections established`

## How it works



