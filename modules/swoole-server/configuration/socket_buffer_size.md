## Configuration

### socket_buffer_size

Set the buffer size of socket.

This configuration is to set the max memory size of connection. 

#### Usage

```php
$server->set([
    'socket_buffer_size' => 128 * 1024 *1024, //必须为数字
])
```
