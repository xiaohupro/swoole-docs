## Method

### swoole_server->exist

#### Prototype

```php
bool swoole_server->exist(int $fd)
```

#### Illustration

Check whether the `$fd` which indicates a TCP client is existed.

#### Parameter

* `$fd`	the id number of client

#### Return

the existence of `$fd` client

#### Example
