## Swoole HTTP server

### Property

#### swoole_http_request->$header

The `swoole_http_request->$header` is an array which contains the information of http request.

All the keys of this array is lowercase.

##### Example

```php
echo $request->header['host'];
echo $request->header['accept-language'];
```
