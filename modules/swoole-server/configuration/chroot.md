## Configuration

### chroot

Redirect the root path of worker process.

This configuration is to separate the operation to the file system in the worker process from the real file system.

#### Usage

```php
$serv->set(array('chroot' => '/data/server/'));
```
