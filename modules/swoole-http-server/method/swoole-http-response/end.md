## Swoole HTTP server

### swoole_http_response->end

#### Prototype

```php
swoole_http_response->end(string $html)
```

#### Illustration

Send data for the HTTP request and end the response.

#### Parameter

- `$html` the data to send to the client

> The call of `$response->end` can only be once.

> If the client enables the configuration of keepalive, the connection between the server and the client will maintain.

> If the client doesn't enable the configuration of keepalive, the connection between the server and the client will be closed.
