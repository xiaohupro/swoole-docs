## Method

### swoole_server->after

#### Prototype

```php
int swoole_server->after(int $after_time_ms, mixed $callback_function)
```

#### Illustration

Trigger a one time tick in the future. Alias of function *swoole_timer_after()*. You can remove the timer later by calling `swoole_timer_clear`

#### Parameter

* `$time`	the number of millisecond
* `$callable` the function that triggered after with a fixed time delay

#### Return

the timer id which uniquely identifies the timer

#### Example
