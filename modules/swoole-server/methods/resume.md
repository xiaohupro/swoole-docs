## Method

### swoole_server->resume

#### Prototype

```php
bool swoole_server->resume(int $fd)
```

#### Illustration

Resume the data receiving for the `$fd` client..

> Only available in SWOOLE_BASE mode.

#### Parameter

* `$fd`	the id number of client

#### Return

the result of resuming 

#### Example
