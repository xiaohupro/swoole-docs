# Swoole TCP/UDP client

Swoole client provide the wrapper of TCP/UDP sockets client side API. 

Compare with PHP *stream* functions, *swoole_client* is more advanced:

* There is a bug in stream function, 
* fread has the limitation length of 8129, can't support big UDP packet
* swoole_client supports waitall, able to read all the data if the packet length is known.
* swoole_client supports UDP connect, there will be no UDP packets mixing up issues.
* swoole_client has better performance.
* swoole_client supports async non-blocking callback, along with sync blocking and select API.

### Events

* Connect
* Receive
* Close
* Error 
* BufferFull
* BufferEmpty

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

### Methods

#### swoole_client->__construct(int $sock_type, int $is_sync = SWOOLE_SOCK_SYNC, string $key);

Create Swoole sync or async TCP/UDP client, with or without SSL.

Example:

Create persistent TCP connection in php-fpm or apache php:

``` php
<?php
$cli = new swoole_client(SWOOLE_TCP | SWOOLE_KEEP);
```

#### swoole_client->set(array $settings);

Set the Swoole client parameters before the connection is established.

Examples:

``` php
<?php

// Check EOF
$client->set(array(
    'open_eof_check' => true, // if check the EOF
    'package_eof' => "\r\n\r\n", // EOF
    'package_max_length' => 1024 * 1024 * 2,
));

// Check package length
$client->set(array(
    'open_length_check'     => 1,
    'package_length_type'   => 'N',
    'package_length_offset' => 0,       // The offset of package length variable
    'package_body_offset'   => 4,       // The offset of body of the package
    'package_max_length'    => 2000000,  // The max length of the package
));

// Set the socket buffer size
$client->set(array(
    'socket_buffer_size'     => 1024*1024*2, // 2MB buffer size
));

// Turn off the Nagle TCP algorithm
$client->set(array(
    'open_tcp_nodelay'     =>  true,
));

// Setup SSL files
$client->set(array(
    'ssl_cert_file'     =>  $your_ssl_cert_file_path,
    'ssl_key_file'     =>  $your_ssl_key_file_path,
));

// Setup local TCP address
$client->set(array(
    'bind_address'     =>  '192.168.1.100',
    'bind_port'     =>  36002,
));

// Setup socks5 proxy
$client->set(array(
    'socks5_host'     =>  '192.168.1.100',
    'socks5_port'     =>  1080,
    'socks5_username' => 'username',
    'socks5_password' => 'password',
));
```

#### int swoole_client::on(string $event, mixed $callback);

> Only can be used in async mode.

Set the callback functions for the events:

* connect
* receive
* close
* error 
* BufferFull
* BufferEmpty

> connect/close events will be emitted immediately when UDP client is created or closed.

#### bool $swoole_client->connect(string $host, int $port, float $timeout = 0.1, int $flag = 0)

Connect to the remote TCP/UDP port.

Example:

``` php
<?php
if ($cli->connect('127.0.0.1', 9501)) {
      $cli->send("data");
} else {
      echo "connect failed.";
}
```

#### bool swoole_client->isConnected()

Check if the connection is established.

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

#### swoole_client->getSocket();

Get the TCP socket of the connection.

Example:

``` php
<?php
$socket = $client->getSocket();
if (!socket_set_option($socket, SOL_SOCKET, SO_REUSEADDR, 1)) {
    echo 'Unable to set option on socket: '. socket_strerror(socket_last_error()) . PHP_EOL;
}
```

#### swoole_client->getsockname();

Get the local socket name of the connection.

#### swoole_client->getpeername();

Get the remote socket name of the connection.

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
