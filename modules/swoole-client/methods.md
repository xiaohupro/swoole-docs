# Swoole TCP/UDP client

## Methods List

If the swoole client wants to enable the SSL, it needs to compile swoole with `enable-openssl` or `with-openssl-dir` and adds `SWOOLE_SSL` to the constructor parameter of class `swoole_client`. 

```php
$client = new Swoole\Client(SWOOLE_TCP | SWOOLE_ASYNC | SWOOLE_SSL);
```

### Table of Contents

- [swoole_client::__construct](/modules/swoole-client/methods/construct.md)
- [swoole_client->set(array $setting)](/modules/swoole-client/methods/set.md)
