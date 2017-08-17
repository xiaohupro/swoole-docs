## Swoole Server

### Methods List

#### Table of Contents

- [swoole_server::__construct](/modules/swoole-server/methods/construct.md)
- [swoole_server->set(array $setting)](/modules/swoole-server/methods/set.md)
- [swoole_server->on(string $event, mixed $callback)](/modules/swoole-server/methods/on.md)
- [swoole_server->addListener(string $host, int $port, $type = SWOOLE_SOCK_TCP)](/modules/swoole-server/methods/addListener.md)
- [swoole_server->listen(string $host, int $port, $type = SWOOLE_SOCK_TCP)](/modules/swoole-server/methods/listen.md)
- [swoole_server->addProcess(swoole_process $process)](/modules/swoole-server/methods/addProcess.md)
- [swoole_server->start()](/modules/swoole-server/methods/start.md)
- [swoole_server->reload(bool $only_reload_taskworkrer = false)](/modules/swoole-server/methods/reload.md)
- [swoole_server->stop($worker_id)](/modules/swoole-server/methods/stop.md)
- [swoole_server->shutdown()](/modules/swoole-server/methods/shutdown.md)
- [swoole_server->tick(int $intval_ms, mixed $callback_function)](/modules/swoole-server/methods/tick.md)
- [swoole_server->after(int $after_time_ms, mixed $callback_function)](/modules/swoole-server/methods/after.md)
- [swoole_server->defer(callable $callback)](/modules/swoole-server/methods/defer.md)
- [swoole_server->clearTimer(int $timer_id)](/modules/swoole-server/methods/clearTimer.md)
- [swoole_server->close(int $fd, bool $reset = false)](/modules/swoole-server/methods/close.md)
- [swoole_server->send(int $fd, string $data, int $reactorThreadId = 0)](/modules/swoole-server/methods/send.md)
- [swoole_server->sendfile(int $fd, string $filename, int $offset =0, int $length = 0)](/modules/swoole-server/methods/sendfile.md)
- [swoole_server->sendto(string $ip, int $port, string $data, int $server_socket = -1)](/modules/swoole-server/methods/sendto.md)
- [swoole_server->sendwait(int $fd, string $send_data)](/modules/swoole-server/methods/send_wait.md)
- [swoole_server->sendMessage(string $message, int $dst_worker_id)](/modules/swoole-server/methods/sendMessage.md)
- [swoole_server->exist(int $fd)](/modules/swoole-server/methods/exit.md)
- [swoole_server->pause(int $fd)](/modules/swoole-server/methods/pause.md)
- [swoole_server->resume(int $fd)](/modules/swoole-server/methods/resume.md)
- [swoole_server->connection_info(int $fd, int $from_id, bool $ignore_close = false)](/modules/swoole-server/methods/connection_info.md)
- [swoole_server->connection_list(int $start_fd = 0, int $pagesize = 10)](/modules/swoole-server/methods/connection_list.md)
- [swoole_server->bind(int $fd, int $uid)](/modules/swoole-server/methods/bind.md)
- [swoole_server->stats()](/modules/swoole-server/methods/stats.md)
- [swoole_server->task(mixed $data, int $dst_worker_id = -1)](/modules/swoole-server/methods/task.md)
- [swoole_server->taskwait(mixed $task_data, float $timeout = 0.5, int $dst_worker_id = -1)](/modules/swoole-server/methods/taskwait.md)


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
