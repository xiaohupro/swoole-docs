## Method

### swoole_server->tick

#### Prototype

```php
int swoole_server->tick(int $time, mixed $callable)
```

#### Illustration

Trigger a timer tick by interval. Alias of function *swoole_timer_tick()*. You can remove the timer later by calling `swoole_timer_clear`

#### Parameter

* `$time`	the number of millisecond
* `$callable` the function that triggered repeatedly with a fixed time delay between each call

#### Return

the timer id  which uniquely identifies the timer

#### Example

Use the `swoole_server->tick` in onReceive
```php
function onReceive($server, $fd, $from_id, $data) {
	$server->tick(1000, function() use ($server, $fd) {
		$server->send($fd, "hello world");
	});
}
```

Use the `swoole_server->tick` in onWorkerStart
```php
function onWorkerStart(swoole_server $serv, $worker_id)
{
	if (!$serv->taskworker) {
		$serv->tick(1000, function ($id) {
			var_dump($id);
		});
	} else {
		$serv->addtimer(1000);
	}
}
```
