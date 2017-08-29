# Swoole TCP/UDP client

## Constants List

### swoole_client::MSG_WAITALL

This constant is used in the second parameter of method `swoole_client->recv`. It means that the swoole client will not return untill received the data of specified length.

```php
$client->recv(8192, swoole_client::MSG_PEEK | swoole_client::MSG_WAITALL);
```

### swoole_client::MSG_DONTWAIT

Receive the data in non-blocking mode.

### swoole_client::MSG_PEEK

If this constant has been added to the parameter, the recv of client will not change the pointer of recv data and read data from the same offset in next time.

### swoole_client::MSG_OOB

Receive the out-of-band data.
