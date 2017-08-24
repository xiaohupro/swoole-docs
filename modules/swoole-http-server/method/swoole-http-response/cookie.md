## Swoole HTTP server

### swoole_http_response->cookie

#### Prototype

```php
swoole_http_response->cookie(string $key, string $value = '', int $expire = 0 , string $path = '/', string $domain  = '', bool $secure = false , bool $httponly = false);
```

#### Illustration

Amount to `setcookie` of PHP.


> This method must be called before the end method
