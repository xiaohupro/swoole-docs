# Swoole scheduler

Schedule functions to run at set intervals, accurate to milliseconds.

### Methods

#### swoole_timer_tick($after_duration_ms, $callback, $param = NULL);

Trigger a timer tick by interval. Alias of function *swoole_timer_tick()*.

Example:

``` php
<?php
swoole_timer_tick(1000, function() {
    echo "hello world\n";
});
```

#### swoole_timer_after($after_duration_ms, $callback, $param = NULL);

Trigger a one time callback function in the future.

#### boolean swoole_timer_clear($id);

Cancel the timer tick or one time tick. Alias of function *swoole_timer_clear*.

#### boolean swoole_timer_exists($id);

Check if the timer is existed.