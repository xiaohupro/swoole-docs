# Swoole Redis Server

## Methods

### swoole_redis_server->setHandler

#### Prototype

```php
function swoole_redis_server->setHandler(string $command, callable $callback)
```

#### Illustration

Set the handling function of redis command. 

#### Parameter

- `$command` the redis command

- `$callback` the function to handle the redis command. The return data of this function must is in form of Redis. You can the method `swoole_redis_server::format` to make the return data.

#### Example

```php
$server = new swoole_redis_server('127.0.0.1', 9501);

//synchronous mode
$server->setHandler('Set', function($fd, $data) {
    $server->array($data[0], $data[1]);
    return swoole_redis_server::format(Server::INT, 1);
});

//asynchronous mode
$server->setHandler('Get', function ($fd, $data) use ($server) {
    $db->query($sql, function($db, $result) use ($fd) {
        $server->send($fd, Server::format(Server::LIST, $result));
    });
});

$server->start();
```
