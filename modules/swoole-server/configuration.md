## Swoole Server

### Configuration

#### ssl_cert_file
#### ssl_key_file

> It must add `--enable-openssl` to the support for ssl when you compile the swoole

To enable ssl, it should set the file path of the cert file and the key file.

```php
$server = new swoole_server("0.0.0.0", 9501, SWOOLE_PROCESS, SWOOLE_SOCK_TCP | SWOOLE_SSL);
$server->set(array(
    'ssl_cert_file' => __DIR__ . '/config/ssl.cert',
    'ssl_key_file' => __DIR__ . '/config/ssl.key',
));
```

 - The web browser must believes in the credential before browsing the webpage
 - In the websock application, the part starting the connection of websocket must use https
 - The file must in the extension 

#### ssl_method

#### ssl_ciphers
