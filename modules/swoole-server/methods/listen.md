## Method

### swoole_server->listen

#### Prototype

```php
mixed swoole_server->listen(string $host, int $port, $type = SWOOLE_SOCK_TCP);
```

#### Illustration

Alias of bool swoole_server->addlistener(string $host, int $port, int $type);
