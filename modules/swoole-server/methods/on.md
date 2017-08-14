## Method

### swoole_server->on 

#### Prototype

```php
bool swoole_server->on(string $event, mixed $callback)
```

#### Illustration

Register callback function for the event

#### Parameter

* `$event` the string of event to be registered
* `$callback` the callable type variable

> Check [the full list of events](/modules/swoole-server/callback-functions.md)

> Check [the four types of callbacks](/modules/swoole-server/common-problems.md)

#### Return

the result if it has been registered successfully 

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
