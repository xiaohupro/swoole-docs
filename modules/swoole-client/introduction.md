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






#### int $swoole_client->send(string $data);

Send data to the remote TCP socket.

#### bool swoole_client->sendto(string $ip, int $port, string $data);

Send data to the remote UDP address.

#### bool swoole_client->sendfile(string $filename, int $offset = 0, int $length = 0)

Send file to the remote TCP socket.

> This is a wrapper of the Linux *sendfile* system call.

#### string $swoole_client->recv(int $size = 65535, int $flags = 0);

Receive data from the remote socket.

#### bool $swoole_client->close(bool $force = false);

Close the connection.


#### swoole_client->getPeerCert()

Get the Cert of the remote server.

#### swoole_client->sleep()

Remove the TCP client from system event loop.

#### swoole_client->wakeup()

Add the TCP client into the system event loop.

Example:

``` php
<?php
$client->on("receive", function(swoole_client $cli, $data){
    $cli->sleep();
    swoole_timer_after(5000, function() use ($cli) {
        $cli->wakeup();
    });
});
```

#### swoole_client->enableSSL()

Enable the SSL for the TCP client.

#### swoole_client->pipe($socket);

Examples:

Sync TCP client with SSL:

``` php
<?php
$client = new swoole_client(SWOOLE_SOCK_TCP);
if (!$client->connect('127.0.0.1', 9501, -1))
{
    exit("connect failed. Error: {$client->errCode}\n");
}
$client->send("hello world\n");
echo $client->recv();

if ($client->enableSSL())
{
    $client->send("hello world\n");
    echo $client->recv();
}
$client->close();
```

Async TCP client with SSL:

``` php
<?php
$client = new swoole_client(SWOOLE_SOCK_TCP, SWOOLE_SOCK_ASYNC);
$client->on("connect", function(swoole_client $cli) {
    $cli->send("hello world\n");
});
$client->on("receive", function(swoole_client $cli, $data) {
    echo "Receive: $data";
    $cli->send(str_repeat('A', 10)."\n");

    $cli->enableSSL(function($client) { 
        $client->send("hello");
    })
});
$client->on("error", function(swoole_client $cli){
    echo "error\n";
});
$client->on("close", function(swoole_client $cli){
    echo "Connection close\n";
});
$client->connect('127.0.0.1', 9501);
```
