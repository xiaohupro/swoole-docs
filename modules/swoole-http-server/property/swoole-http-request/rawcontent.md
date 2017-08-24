## Swoole HTTP server

### Method

#### swoole_http_request->rawContent

The `swoole_http_request->$rawContent` is an array which amounts to the `$_POST` of PHP.

##### Example

```php
echo $request->post['hello'];
var_dump($request->post);
```
