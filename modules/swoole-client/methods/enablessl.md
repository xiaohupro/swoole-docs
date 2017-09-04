# Swoole TCP/UDP client

## Methods 

### swoole_client->enableSSL

#### Prototype

```php
bool swoole_client->enableSSL(mixed $var);
```

#### Illustration

If the client hasn't enabled the SSL in the construction and has connnected to the server, you can enable the SSL for the TCP client by this method.

#### Parameter

For sync TCP client, it should not pass parameter to this method and this method wouldn't return until the process of enabling SSL finished.

For async TCP client, it should pass the callback function which is called after the process of enabling SSL finished. 

#### Return

bool

#### Example

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
