# Swoole WebSocket server

## Events and Callback Functions

### onHandShake

This event happens when the websocket connection start the handshake process. The `swoole_websocket_server` has built-in callback function registered for event `handshake`. But you can also choose to custom your callback function for event `handshake`.

#### Example

```php
function onHandShake(swoole_http_request $request, swoole_http_response $response)
```

- If the return of function is `true`, the handshake is successful.

> The callback function for event `handshake` is optional.

> If the callback function for event `handshake` has been customed, the event `open` would not be triggered. 

> The built-in protocol of handshake is `Sec-WebSocket-Version: 13`, it needs to implemen t the process of handshake when the browser is in low-version.


#### Example Code

```php
$server->on('handshake', function (\swoole_http_request $request, \swoole_http_response $response) {
	$secWebSocketKey = $request->header['sec-websocket-key'];
	$patten = '#^[+/0-9A-Za-z]{21}[AQgw]==$#';
	
	if (0 === preg_match($patten, $secWebSocketKey) || 16 !== strlen(base64_decode($secWebSocketKey))) {
		$response->end();
		return false;
	}
	
	echo $request->header['sec-websocket-key'];
	
	$key = base64_encode(sha1($request->header['sec-websocket-key'] . '258EAFA5-E914-47DA-95CA-C5AB0DC85B11', true));

	$headers = [
		'Upgrade' => 'websocket',
		'Connection' => 'Upgrade',
		'Sec-WebSocket-Accept' => $key,
		'Sec-WebSocket-Version' => '13',
	];

	// WebSocket connection to 'ws://127.0.0.1:9502/'
	// failed: Error during WebSocket handshake:
	// Response must not include 'Sec-WebSocket-Protocol' header if not present in request: websocket
	if (isset($request->header['sec-websocket-protocol'])) {
		$headers['Sec-WebSocket-Protocol'] = $request->header['sec-websocket-protocol'];
	}

	foreach ($headers as $key => $val) {
		$response->header($key, $val);
	}

	$response->status(101);
	$response->end();
	echo "connected!" . PHP_EOL;
	return true;
});

```
