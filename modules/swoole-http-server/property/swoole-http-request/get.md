## Swoole HTTP server

### Property

#### swoole_http_request->$get

The `swoole_http_request->$get` is an array which amounts to the `$_GET` of PHP.

##### Example

```php
echo $request->get['hello'];
var_dump($request->get);
```

> The max number of GET parameters is 128
