## Method

### swoole_server->sendwait

#### Prototype

```php
bool swoole_server->sendwait(int $fd, string $send_data)
```
#### Illustration

Send data to the remote socket in the blocking way.

> Only available in SWOOLE_BASE mode.

#### Parameter

* `$fd`	the id number of client
* `$send_data` the data to send

#### Return

the result of sending data

#### Example
