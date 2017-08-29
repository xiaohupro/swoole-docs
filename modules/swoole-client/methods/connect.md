# Swoole TCP/UDP client

## Methods 

### swoole_client->connect

#### Prototype

```php
bool swoole_client->connect(string $host, int $port, float $timeout = 0.1, int $flag = 0)
```

#### Illustration

Connect to the remote TCP/UDP port.

#### Parameter

* `$host`	  the ip address the client connects to
* `$port`     the port the client connects to
* `$timeout`  the timeout(second) of connect/send/recv, the dafault value is 0.1s
* `$flag`     if the type of client is UCP,  

#### Return


#### Example

``` php
<?php
if ($cli->connect('127.0.0.1', 9501)) {
      $cli->send("data");
} else {
      echo "connect failed.";
}
```
