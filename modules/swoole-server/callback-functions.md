## Swoole Server

### Events List

The swoole is an an high-performance network framework uses an event-driven, asynchronous, non-blocking I/O model makes it scalable and efficient. All the business logic is written in the callback functions of events. When a certain event is triggered, the swoole will call the callback function registered for the event. 

There are thirteen types of event listed in the below table of contents.

#### Table of Contents

 - [onStart](/modules/swoole-server/callback-functions/onstart.md)
 - [onShutdown](/modules/swoole-server/callback-functions/onshutdown.md)
 - [onWorkerStart](/modules/swoole-server/callback-functions/onworkerstart.md)
 - [onWorkerStop](/modules/swoole-server/callback-functions/onworkerstop.md)
 - [onTimer](/modules/swoole-server/callback-functions/ontimer.md)
 - [onConnect](/modules/swoole-server/callback-functions/onconnect.md)
 - [onReceive](/modules/swoole-server/callback-functions/onreceive.md)
 - [onPacket](/modules/swoole-server/callback-functions/onpacket.md)
 - [onClose](/modules/swoole-server/callback-functions/onclose.md)
 - [onBufferFull](/modules/swoole-server/callback-functions/onbufferfull.md)
 - [onBufferEmpty](/modules/swoole-server/callback-functions/onbufferempty.md)
 - [onTask](/modules/swoole-server/callback-functions/ontask.md)
 - [onFinish](/modules/swoole-server/callback-functions/onfinish.md)
 - [onPipeMessage](/modules/swoole-server/callback-functions/onpipemessage.md)
 - [onWorkerError](/modules/swoole-server/callback-functions/onworkererror.md)
 - [onManagerStart](/modules/swoole-server/callback-functions/onmanagerstart.md)
 - [onManagerStop](/modules/swoole-server/callback-functions/onmanagerstop.md)

#### Order of events

- All the callback functions of events are triggered after the start of swoole server.

- The last event of swoole server is `onShutdown` when the swoole server shutdowns.

- After starting the swoole server, the callback functions of `onStart/onManagerStart/onWorkerStart` are triggered in different process.


#### Catch Exception

The swoole doesn't support the `set_exception_handler` function.

If there is the logic of throwing exception in your code, it must add the `try/catch` in the very beginning of callback function.

```php
$serv->on('Timer', function() {
    try
    {
        //some code
    }
    catch(Exception $e)
    {
        //exception code
    }
}
```

#### Example

Example of registering event callback functions:

``` php
<?php
$server = new swoole_server("127.0.0.1", 9501, SWOOLE_BASE, SWOOLE_SOCK_TCP);
$server->on('WorkerStart', function($serv, $workerId) {
    var_dump(get_included_files());
});
```
