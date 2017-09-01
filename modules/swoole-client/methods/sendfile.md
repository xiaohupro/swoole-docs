# Swoole TCP/UDP client

## Methods 

### swoole_client->sendfile

#### Prototype

```php
bool swoole_client->sendfile(string $filename, int $offset = 0, int $length = 0)
```

#### Illustration

Send file to the remote TCP socket.

> This is a wrapper of the Linux *sendfile* system call.

#### Parameter

- `$filename` the path of file to send

- `$offset` the offset of file to start send

- `$length` the length of file to send. The default value is the whole length of file.

#### Return

bool

If the file doesn't exist, the return is false. 
