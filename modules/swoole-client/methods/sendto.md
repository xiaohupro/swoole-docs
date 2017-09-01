# Swoole TCP/UDP client

## Methods 

### swoole_client->sendto

#### Prototype

```php
bool swoole_client->sendto(string $ip, int $port, string $data);
```

#### Illustration

Send data to the remote UDP address. The swoole client should be type of SWOOLE_SOCK_UDP or SWOOLE_SOCK_UDP6.

#### Parameter

- `$ip` the ip address of remote host, ipv4 or ipv6

- `$port` the port number of remote host

- `$data` the data to send which should be less-than 64K.

#### Return

bool
