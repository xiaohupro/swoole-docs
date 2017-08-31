# Swoole TCP/UDP client

## Methods 

### swoole_client->getPeerName

#### Prototype

```php
array swoole_client->getPeerName();
```

#### Illustration

Get the remote socket name of the connection.

#### Parameter

void

#### Return

The array of remote socket host and port

``` php
array('host' => '127.0.0.1', 'port' => 53652)
```
