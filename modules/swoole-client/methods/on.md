# Swoole TCP/UDP client

## Methods 

### swoole_client->on

#### Prototype

```php
int swoole_client::on(string $event, mixed $callback)
```

#### Illustration

> Only can be used in async mode.

Set the callback functions for the events:

* connect
* receive
* close
* error 
* BufferFull
* BufferEmpty

> connect/close events will be emitted immediately when UDP client is created or closed.

#### Parameter

* `$event`	  the event to be registered with callback function
* `$callback` the callback function

#### Return


#### Example

```php
<?php
$client = new swoole_client(SWOOLE_SOCK_TCP, SWOOLE_SOCK_ASYNC);
$client->on("connect", function(swoole_client $cli) {
    $cli->send("GET / HTTP/1.1\r\n\r\n");
});
$client->on("receive", function(swoole_client $cli, $data){
    echo "Receive: $data";
    $cli->send(str_repeat('A', 100)."\n");
    sleep(1);
});
$client->on("error", function(swoole_client $cli){
    echo "error\n";
});
$client->on("close", function(swoole_client $cli){
    echo "Connection close\n";
});
$client->connect('127.0.0.1', 9501);

```
