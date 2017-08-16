## Method

### swoole_server->sendfile

#### Prototype

```php
bool swoole_server->sendfile(int $fd, string $filename, int $offset = 0, int $length = 0)
```

#### Illustration

Send large size data or files to the remote TCP socket. A wrapper of the *sendfile* system call.

#### Parameter

* `$fd`	the id number of client
* `$filename` the path of file to send
* `$offset` the start offset of file to send. The default of this parameter is 0
* `$length` the length of file to send. The default of this parameter is the whole length of file

#### Return

the timer id which uniquely identifies the timer

#### Example

``` php
<?php
$server->sendfile($fd, __DIR__.'/test.jpg');
```
