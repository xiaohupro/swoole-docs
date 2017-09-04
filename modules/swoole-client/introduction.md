# Swoole TCP/UDP client

Swoole client provide the wrapper of TCP/UDP sockets client side API. 

Compare with PHP *stream* functions, *swoole_client* is more advanced:

* There is a bug in stream function, 
* fread has the limitation length of 8129, can't support big UDP packet
* swoole_client supports waitall, able to read all the data if the packet length is known.
* swoole_client supports UDP connect, there will be no UDP packets mixing up issues.
* swoole_client has better performance.
* swoole_client supports async non-blocking callback, along with sync blocking and select API.

### Table of Contents

* [Methods List](/modules/swoole-client/methods.md)

* [Callback functions](/modules/swoole-client/callback-functions.md)

* [Properties List](/modules/swoole-client/properties.md)

* [Predefined Constants](/modules/swoole-client/predefined-constants.md)

* [Configurations List](/modules/swoole-client/configuration.md)

* [Common Problems](/modules/swoole-client/common-problems.md)

### Examples

A simple sync TCP client:

``` php
<?php
$client = new swoole_client(SWOOLE_SOCK_TCP);
if (!$client->connect('127.0.0.1', 9501, -1))
{
    exit("connect failed. Error: {$client->errCode}\n");
}
$client->send("hello world\n");
echo $client->recv();
$client->close();
```

A simple async TCP client:

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

> Note, the async TCP client can not be used in PHP-FPM or Apache mode, only can be used in Swoole server.
