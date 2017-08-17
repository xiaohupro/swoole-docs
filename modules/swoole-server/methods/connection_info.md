## Method

### swoole_server->connection_info

#### Prototype

```php
mixed swoole_server->connection_info(int $fd, int $from_id, bool $ignore_close = false)
```

#### Illustration

Get the connection info, alias of function *swoole_server->getClientInfo()*.

#### Parameter

* `$fd`	the id number of client
* `$from_id` this parameter is needed, the swoole server is type of UDP
* `$ignore_close` this method will return the information of connection even if the connection is closed

#### Return

the array of information of the `$fd` client 

if the `$fd` client dosen't exist, the result is false 

#### Example

``` php
<?php
$fdinfo = $serv->connection_info($fd);
var_dump($fdinfo);
array(5) {
  ["from_id"]=>
  int(3)
  ["server_fd"]=>
  int(14)
  ["server_port"]=>
  int(9501)
  ["remote_port"]=>
  int(19889)
  ["remote_ip"]=>
  string(9) "127.0.0.1"
  ["connect_time"]=>
  int(1390212495)
  ["last_time"]=>
  int(1390212760)
}

$udp_client = $serv->connection_info($fd, $from_id);
var_dump($udp_client);
```
