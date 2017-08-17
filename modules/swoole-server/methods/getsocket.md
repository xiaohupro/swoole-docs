## Method

### swoole_server->getSocket

#### Prototype

```php
resource swoole_server->getSocket()
```

#### Illustration

Get socket and update the options of the socket.

> This method is based on the extension sockets and it needs to add the compiling configuration `--enable-sockets`

#### Parameter

void

#### Return

the handler of sockets resource

#### Example

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
