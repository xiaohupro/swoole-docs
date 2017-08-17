## Configuration 

#### ssl_method

Set the algorithm of ssl. The algorithm of client and server must be same otherwise the handshake of websocket will fail.
The default algorithm is `SWOOLE_SSLv23_METHOD`

```php
$server->set(array(
    'ssl_method' => SWOOLE_SSLv3_CLIENT_METHOD, // this configuration is available for the swoole whose version is higher than 1.7.20
));
```
