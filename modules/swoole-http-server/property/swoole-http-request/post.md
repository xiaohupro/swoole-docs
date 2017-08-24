## Swoole HTTP server

### Property

#### swoole_http_request->$post

The `swoole_http_request->$post` is an array which amounts to the `$_POST` of PHP.

##### Example

```php
echo $request->post['hello'];
var_dump($request->post);
```
