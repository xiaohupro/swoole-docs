## Swoole HTTP server

### swoole_http_request->rawContent

#### Prototype

```php
string swoole_http_request->rawContent();
```

#### Illustration

Get the raw POST body. This method is used for the POST which isn't in form of `application/x-www-form-urlencoded`.

#### Return 

Return the raw post data.

> You can set the configuration `http_parse_post` to control the analysis of POST data. 
