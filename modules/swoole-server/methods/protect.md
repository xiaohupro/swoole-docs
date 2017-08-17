## Method

### swoole_server->protect

#### Prototype

```php
swoole_server->protect(int $fd, bool $value = true)
```

#### Illustration

Protect the `$fd` from being closed by the thread of checking heart beat

#### Parameter

* `$fd`	the id number of client
* `$value` if true, protect the `$fd`. If false, remove the protect from `$fd`

#### Return


#### Example
