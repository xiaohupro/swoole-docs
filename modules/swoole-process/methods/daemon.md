# Swoole Process Manager

## Methods 

### swoole_process::daemon

#### Prototype

```php
bool swoole_process->daemon(bool $nochdir = true, bool $noclose = true);
```

#### Illustration

Change the process to be a daemon process.

#### Parameter

* $nochdir: whether change the current path.

* $noclose: whether close the standard I/O of the process.

#### Return

bool
