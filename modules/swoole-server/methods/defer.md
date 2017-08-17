## Method

### swoole_server->defer

#### Prototype

```php
void swoole_server->defer(callable $callback)
```

#### Illustration

Delay execution of the callback function at the end of current *EventLoop*. Alias of function *swoole_event_defer()*.

#### Parameter

* `$callback` the function that defers to execute

#### Return

void

#### Example

```php
function query($server, $db) {
	$server->defer(function() use ($db) {
		$db->close();
	});
}
```
