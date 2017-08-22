## Events and Callback functions 

### onBufferEmpty

The event `bufferempty` happens when the buffer watermark is lowest.

#### Example

```php
function onBufferEmpty(Swoole\Server $serv, int $fd)
```
-  Set the configuration `server->buffer_low_watermark` to control the buffer low watermark
- When the event `bufferempty` is triggered, it could send data to client.
