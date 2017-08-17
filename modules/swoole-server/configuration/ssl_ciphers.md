## Configuration 

#### ssl_ciphers

Set the `ssl_ciphers` to change the default encryption algorithm of openssl. The default encryption algorithm of openssl is `EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH`

```php
$server->on(array(
    'ssl_ciphers' => 'ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP', // the swoole use the default algorithm when the `ssl_ciphers` is empty
));
```
