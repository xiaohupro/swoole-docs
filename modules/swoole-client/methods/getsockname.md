# Swoole TCP/UDP client

## Methods 

### swoole_client->getSockName

#### Prototype

```php
array swoole_client->getSockName();
```

#### Illustration

Get the local socket name of the connection.

#### Parameter

void

#### Return

The array of local socket host and port

``` php
array('host' => '127.0.0.1', 'port' => 53652)
```
