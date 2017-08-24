## Swoole HTTP server

### swoole_http_response->sendfile

#### Prototype

```php
swoole_http_response->sendfile(string $filename, int $offset = 0, int $length = 0);
```

#### Illustration

Response the file content to the client.

#### Parameter

- `$filename` the file path to send. If there is no this file, the sendfile will fail.

- `$offset` the start offset of file to send.

- `$length` the length of data to send. The default value is the whole length of file.

> Before the call of this method, it has to set content type by `$response->header()`.

> Before the call of this method, it must not call `$response->write`

> After the call of this method, it will call `$response->end()` automatically.

> `$response->sendfile` doesn't support gzip compression.

#### Example

```php
$response->header('Content-Type', 'image/jpeg');
$response->sendfile(__DIR__.$request->server['request_uri']);
```
