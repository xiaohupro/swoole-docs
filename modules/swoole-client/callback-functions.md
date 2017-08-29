# Swoole TCP/UDP client

## Events and Callback-functions List

There is no connect and close connection event for UDP. If you have setted the callback function for event `connect`, it will be called immediately after the UDP client is created.

If you have setted the callback function for event `close`, it will be called immediately after the UDP client is closed.

### Table of Contents

- onConnect
- onError
- onReceive
- onClose
- onBufferFull
- onBufferEmpty

#### onConnect

`connect` event happens when the client connect to the server successfully.

```php
function onConnect(swoole_client $client)
```

For TCP client, it must set the callback function for this event. 

#### onError
#### onReceive
#### onClose
#### onBufferFull
#### onBufferEmpty
