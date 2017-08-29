# Swoole TCP/UDP client

## Methods 

### swoole_client::__construct 

#### Prototype

```php
swoole_client->__construct(int $sock_type, int $is_sync = SWOOLE_SOCK_SYNC, string $key);
```

#### Illustration

Create Swoole sync or async TCP/UDP client, with or without SSL.

#### Parameter

* `$sock_type`	the type of socket
* `$is_sync`    set the client to be synchronous or asynchronous 
* `$key`        the key used for long connection, the default key is IP:PORT. the connection which has the same key will be reused

#### Return

the swoole_client object

#### Example

Create persistent TCP connection in php-fpm or apache php:

``` php
<?php
$cli = new swoole_client(SWOOLE_TCP | SWOOLE_KEEP);
```
