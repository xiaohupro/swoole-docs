# Swoole TCP/UDP client

## Methods List

If the swoole client wants to enable the SSL, it needs to compile swoole with `enable-openssl` or `with-openssl-dir` and adds `SWOOLE_SSL` to the constructor parameter of class `swoole_client`. 

```php
$client = new Swoole\Client(SWOOLE_TCP | SWOOLE_ASYNC | SWOOLE_SSL);
```

### Table of Contents

- [swoole_client::__construct](/modules/swoole-client/methods/construct.md)
- [swoole_client->set(array $setting)](/modules/swoole-client/methods/set.md)
- [swoole_client->on(string $event, mixed $callback)](/modules/swoole-client/methods/on.md)
- [swoole_client->connect(string $host, int $port, float $timeout = 0.1, int $flag = 0)](/modules/swoole-client/methods/connect.md)
