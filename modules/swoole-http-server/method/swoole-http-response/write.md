## Swoole HTTP server

### swoole_http_response->write

#### Prototype

```php
bool swoole_http_response->write(string $data);
```

#### Illustration

Enable `chunk` of Http to send data to client. Check the [reference material](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Transfer-Encoding) about `chunk` of Http.

#### Parameter

- `$data` the max length of data is 2M

> After this method has been called, the call of `$response->end` can't be passed any parameter. 

> After the call of `$response->end()`, it would send a chunk of length 0 
