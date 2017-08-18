## Configuration

### dispatch_mode

The mode of dispatching connections to worker process.

This parameter only works for the `SWOOLE_PROCESS` mode swoole_server.

- `1`, polling mode. Dispatch the connection to the workers in sequence.

- `2`, fixed mode(default value of `dispatch_mode`). Dispatch the connection to the worker according to the id number of connection. In this mode, the data from the same connection will be handled by the same worker process. 

- `3`, preemptive mode. The swoole will dispatch the connection to the unoccupied worker process.

- `4`, ip mode. Dispatch the connection to the worker according to the ip of client. The dispatch algorithm is `ip2long(ClientIP) % worker_num`

- `5`, uid mode. If the connection has been bound with a uid by [swoole_server->bind](/modules/swoole-server/methods/bind.md), the swoole will dispatch the connection to the worker according to the uid. The dispatch algorithm is `UID % worker_num`. If you want to use a string as a uid, it should convert this string by `crc32($uid)`

#### Usage advice

- stateless server: `3` is advised for synchronous and blocking server, `1` is advised for asynchronous and non-blocking server

- stateful server: `2`, `4`, `5`

If the `dispatch_mode` is `1` or `3`, the event of `connect` and `close` will be shielded.
