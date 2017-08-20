## Configuration

### enable_delay_receive

Enable the delay of receiving new connection.

Once enabled, the client which has been accepted would not be added to the EventLoop automaticlly and only trigger the callback function of the receive event.

The worker process needs to call `$serv->confirm($fd)` to confirm the connection manually and add the connection to the EventLoop. 

#### Usage

```php
// enable `enable_delay_receive`
$serv->set(array(
	'enable_delay_receive' => true,
));

$serv->on("Connect", function ($serv, $fd, $reactorId) {
	$serv->after(2000, function() use ($serv, $fd) {
		// confirm connection and start process data
		$serv->confirm($fd);
	});
});
```
