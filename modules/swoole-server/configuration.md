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
 - The certificate extensions must be PEM and not DER

Convert PEM to DER
```
openssl x509 -in cert.crt -outform der -out cert.der
```
Convert DER to PEM
```
openssl x509 -in cert.crt -inform der -outform pem -out cert.pem
```

#### ssl_method

Set the algorithm of ssl. The algorithm of client and server must be same otherwise the handshake of websocket will fail.
The default algorithm is `SWOOLE_SSLv23_METHOD`

```php
$server->set(array(
    'ssl_method' => SWOOLE_SSLv3_CLIENT_METHOD, // this configuration is available for the swoole whose version is higher than 1.7.20
));
```

#### ssl_ciphers

Set the `ssl_ciphers` to change the default encryption algorithm of openssl. The default encryption algorithm of openssl is `EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH`

```php
$server->on(array(
    'ssl_ciphers' => 'ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP', // the swoole use the default algorithm when the `ssl_ciphers` is empty
));
```
