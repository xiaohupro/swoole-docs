## Swoole HTTP server

### Property

#### swoole_http_request->$files

The `swoole_http_request->$files` is an array which amounts to the `$_FILES` of PHP.

##### Example

```php
var_dump($request->cookie);
Array
(
 [name] => facepalm.jpg
 [type] => image/jpeg
 [tmp_name] => /tmp/swoole.upfile.n3FmFr
 [error] => 0
 [size] => 15476
)
```
> The uploaded files will be deleted after the run of `$response->end()`
