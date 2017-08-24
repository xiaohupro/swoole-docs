## Swoole HTTP server

### Property

#### swoole_http_request->$server

The `swoole_http_request->$server` is an array which contains the information of server and amounts to the `$_SERVER` of PHP.

All the keys of this array is lowercase.

##### Example

```php
echo $request->server['request_time'];
```
