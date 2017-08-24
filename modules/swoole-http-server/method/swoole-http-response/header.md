## Swoole HTTP server

### swoole_http_response->header

#### Prototype

```php
swoole_http_response->header(string $key, string $value)
```

#### Illustration

Set the header content of http response.

#### Parameter

- `$key` the key of header

- `$value` the value of header

#### Example

```php
$responser->header('Content-Type', 'image/jpeg');
```

> This method must be called before the end method
