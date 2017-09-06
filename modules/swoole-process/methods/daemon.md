# Swoole Process Manager

## Methods 

### swoole_process::daemon

#### Prototype

```php
bool swoole_process->daemon(bool $nochdir = true, bool $noclose = true);
```

#### Illustration

Change the process to be a daemon process.

* $nochdir: whether change the current path.
* $noclose: whether close the standard I/O of the process.

#### Parameter

- `$nochdir`

- `$noclose`

#### Return

bool
