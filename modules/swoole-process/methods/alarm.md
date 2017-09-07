# Swoole Process Manager

## Methods 

### swoole_process::alarm

#### Prototype

```php
bool swoole_process->alarm(int $interval_usec, int $type = ITIMER_REAL)
```

#### Illustration

High precision timer which will trigger signal every fixed interval.

#### Parameter

- `$interval_usec`

- `$type`

#### Return

bool

#### Example
```php
<?php
swoole_process::signal(SIGALRM, function () {
    static $i = 0;
    echo "#{$i}\talarm\n";
    $i++;
    if ($i > 20) {
        swoole_process::alarm(-1);
    }
});

//100ms
swoole_process::alarm(100 * 1000);
```
