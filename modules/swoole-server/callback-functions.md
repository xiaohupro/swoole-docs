## Swoole Server

### Events List

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


Example of registering event callback functions:

``` php
<?php
$server = new swoole_server("127.0.0.1", 9501, SWOOLE_BASE, SWOOLE_SOCK_TCP);
$server->on('WorkerStart', function($serv, $workerId) {
    var_dump(get_included_files());
});
```
