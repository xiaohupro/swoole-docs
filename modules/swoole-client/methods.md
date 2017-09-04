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
- [swoole_client->isConnected()](/modules/swoole-client/methods/isconnected.md)
- [swoole_client->getSocket()](/modules/swoole-client/methods/getsocket.md)
- [swoole_client->getSockName()](/modules/swoole-client/methods/getsockname.md)
- [swoole_client->getPeerName()](/modules/swoole-client/methods/getpeername.md)
- [swoole_client->getPeerCert()](/modules/swoole-client/methods/getpeercert.md)
- [swoole_client->send(string $data)](/modules/swoole-client/methods/send.md)
- [swoole_client->sendto(string $ip, int $port, string $data)](/modules/swoole-client/methods/sendto.md)
- [swoole_client->sendfile(string $filename, int $offset = 0, int $length = 0)](/modules/swoole-client/methods/sendfile.md)
- [swoole_client->recv(int $size = 65535, int $flags = 0)](/modules/swoole-client/methods/recv.md)
- [swoole_client->close(bool $force = false)](/modules/swoole-client/methods/close.md)
- [swoole_client->sleep()](/modules/swoole-client/methods/sleep.md)
- [swoole_client->wakeup()](/modules/swoole-client/methods/wakeup.md)
- [swoole_client->enableSSL()](/modules/swoole-client/methods/enablessl.md)
