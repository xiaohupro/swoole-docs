# Swoole TCP/UDP client

## Methods 

### swoole_client->send

#### Prototype

```php
int swoole_client->send(string $data);
```

#### Illustration

Send data to the remote TCP socket.

#### Parameter

- `$data` the data to send which can be text or binary

#### Return

If the client sends data successfully, it returns the length of data sent. Or it returns `false` and sets `$swoole_client->errCode`.

> For sync client, there is no limit for the data to send. 

> For async client, The limit for the data to send is `socket_buffer_size`. 

#### Example
