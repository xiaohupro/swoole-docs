## Swoole Server

### Properties List

#### Table of Contents

- swoole_server::$setting
- swoole_server::$master_pid
- swoole_server::$manager_pid
- swoole_server::$worker_id
- swoole_server::$worker_pid
- swoole_server::$taskworker
- swoole_server::$connections

#### Properties

##### swoole_server::$setting

the setting seted for the swoole server object

```php
$serv = new swoole_server('127.0.0.1', 9501);
$serv->set(array('worker_num' => 4));

echo $serv->setting['worker_num'];
```

##### swoole_server::$master_pid

the pid of master process

##### swoole_server::$manager_pid

the pid of manager process

##### swoole_server::$worker_id

the id number of current worker process or task worker process

##### swoole_server::$worker_pid

the pid of current worker process or task worker process

##### swoole_server::$taskworker

true: current process is task worker process
false: current process isn worker process

##### swoole_server::$connections

the list of all the connections

```php
foreach($server->connections as $fd)
{
    $server->send($fd, "hello");
}

echo "The server has ".count($server->connections). " connections\n";
```
