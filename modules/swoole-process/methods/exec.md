# Swoole Process Manager

## Methods 

### swoole_process->exec

#### Prototype

```php
bool swoole_process->exec(string $execfile, array $args)
```

#### Illustration

Execute system commands:

* $execfile is the path of the command.
* $args are the arguments for the command.

The process will be replaced to be the system command process, but the pipe between the parent process will be kept.

#### Parameter

- `$execfile`

- `$args`

#### Return

bool
