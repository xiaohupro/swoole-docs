## Events and Callback functions 

### onBufferFull

The event `bufferfull` happens when the buffer watermark is highest.

#### Example

```php
function onBufferFull(Swoole\Server $serv, int $fd)
```
-  Set the configuration `server->buffer_high_watermark` to control the buffer high watermark
- When the event `bufferfull` is triggered, it should not send data to client any more.
