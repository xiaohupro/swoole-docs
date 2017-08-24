## Swoole HTTP server

### swoole_http_server->on

#### Prototype

```php
swoole_http_server->on(string $event, $callback)
```

#### Illustration

Register the callback function for the event.

The `swoole_http_server` class inherits from the class `swoole_server`. The `on` method has something different from the `on` method of class `swoole_server`.

- Don't support the event `connect` and `receive`

- Add new event `request`. This event happens when the process receives a complete http request.

#### Example

```php
$http_server->on('request', function(swoole_http_request $request, swoole_http_response $response) {
     $response->end("<h1>hello swoole</h1>");
})
```
When the process receives a complete http request, it will call the callback function registered for this event.

- `$request` the object of class `swoole_http_request`

- `$response` the object of class `swoole_http_response`

- If the callback function hasn't called the `$response->end` function, the swoole will add the call of `$response->end("")` at the end automatically.
