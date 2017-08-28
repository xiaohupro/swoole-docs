# Swoole Redis Server

## Methods

The class `swoole_redis_server` inherits from the class `swoole_server`.

It can call the methods of class `swoole_server` and its own methods. 

The object of class `swoole_redis_server` doesn't need to register the callback function for event `receive`. It needs to use the method `setHandler` to set the corresponding function fo redis command. If the swoole redis server receives the command that hasn't the corresponding function to handle, it responds the message `ERR unknown command '$command'`.

### Table of Contents

* [swoole_redis_server->setHandler](/modules/swoole-redis-server/methods/sethandler.md)

* [swoole_redis_server::format](/modules/swoole-redis-server/methods/format.md)
