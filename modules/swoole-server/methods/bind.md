## Method

### swoole_server->bind

#### Prototype

```php
bool swoole_server->bind(int $fd, int $uid)
```

#### Illustration

Bind the fd with system user UID.

#### Parameter

* `$fd`	the id number of client
* `$callable` the function that triggered after with a fixed time delay

#### Return

the result of binding

#### Example
