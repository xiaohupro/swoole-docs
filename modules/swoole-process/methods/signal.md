# Swoole Process Manager

## Methods 

### swoole_process::signal

#### Prototype

```php
bool swoole_process->signal(int $signo, callable $callback);
```

#### Illustration

Setup signal callback function.

#### Parameter

- `$signo` the signal 

- `$callback` the callback function called when the signal is triggered

#### Return

bool
