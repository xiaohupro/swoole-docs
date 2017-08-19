## Configuration

### pid_file

The file path which the master process id saves in.

#### Usage

```php
$server->set(array(
    'pid_file' => __DIR__.'/server.pid',
));
```
The pid of master process saves in the `pid_file` after the swoole server starts. And this file is deleted after the swoole server stops normally.
