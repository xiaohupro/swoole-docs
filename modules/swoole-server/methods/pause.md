## Method

### swoole_server->pause

#### Prototype

```php
bool swoole_server->pause(int $fd)
```

#### Illustration

Pause the data receiving for the `$fd` client.

> Only available in SWOOLE_BASE mode.

#### Parameter

* `$fd`	the id number of client

#### Return

the result of pausing

#### Example
