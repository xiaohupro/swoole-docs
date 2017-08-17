## Method

### swoole_server->sendto

#### Prototype

```php
bool swoole_server->sendto(string $ip, int $port, string $data, int $server_socket = -1)
```

#### Illustration

Send data to the remote UDP address.

> To use `swoole_server->sendto`, the swoole server has to listen the port of UDP
> To use `swoole_server->sendto` to send data to IPV6, the swoole server has to listen the port of UDP6

#### Parameter

* `$ip`	the string of ip address
* `$port` the integer of port
* `$data` the data to send
* `$server_socket` the swoole server may listen multiple port at the same time, use `$server_socket` to assign the port to use

#### Return

the result of send data

#### Example

``` php
<?php
$server->sendto('220.181.57.216', 9502, "hello world");

$server->sendto('2600:3c00::f03c:91ff:fe73:e98f', 9501, "hello world");
```
