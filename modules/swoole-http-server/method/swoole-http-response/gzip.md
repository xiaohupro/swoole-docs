## Swoole HTTP server

### swoole_http_response->gzip

#### Prototype

```php
swoole_http_response->gzip(int $level = 1);
```

#### Illustration

Enable the gzip of response content. The header about Content-Encoding will be added automatically.

#### Parameter

- `$level` the level of compression

> This method must be called before the end method

> This method needs `zlib`. Install zlib by `sudo apt-get install libz-dev`
