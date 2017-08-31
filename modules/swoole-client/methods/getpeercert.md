# Swoole TCP/UDP client

## Methods 

### swoole_client->getPeerCert

#### Prototype

```php
string swoole_client->getPeerCert();
```

#### Illustration

Get the Cert of the remote server.

> It needs the support of openssl. You should compile swoole with `--enable-openssl`.

#### Parameter

void

#### Return

The Cert of the remote server. You can use the function `openssl_x509_parse` of extension openssl to parse the cert information.
