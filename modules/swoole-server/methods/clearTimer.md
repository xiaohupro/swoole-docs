## Method

### swoole_server->clearTimer

#### Prototype

```php
void swoole_server->clearTimer(int $timer_id)
```

#### Illustration

Cancel the timer tick or one time tick. Alias of function *swoole_timer_clear*.

#### Parameter

* `$timer_id`	the number of timer id which uniquely identifies a timer

#### Return

 void

#### Example
```php
$timer_id = $server->tick(1000, function ($id) use ($server) {
    $server->clearTimer($id);
});
```
