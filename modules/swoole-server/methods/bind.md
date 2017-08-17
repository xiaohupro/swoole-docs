## Method

### swoole_server->bind

#### Prototype

```php
bool swoole_server->bind(int $fd, int $uid)
```

#### Illustration

Bind the fd with system user UID.

The dispatch of different socket connection to the swoole server is influenced by [the configuration of dispatch_mode](/modules/swoole-server/configuration/dispatch_mode.md)

In the default dispatch_mode which is 2, the socket connection may be dispatched to different worker process after reconnetion. You can set the configuration of dispatch_mode to 5 and call `swoole_server->bind` to bind a uid number to socket connection. And then the same uid socket connection will be dispatched to the same worker process.

#### Parameter

* `$fd`	the id number of client
* `$uid` the uid number binded for the client

#### Return

the result of binding

#### Example
