## Events and Callback functions 

### onShutdown

The event `shutdown` happens when the swoole server shutdowns.

Before the event `shutdown`, these operations below happened:

- All threads are closed.
- All the worker processed are closed.
- Cancel the listening on the TCP/UDP port.
- The Reactor is closed.

> Kill the process forcibly, like `kill -9`, will not trigger the call of function registered for `shutdown`. It needs to send `SIGTREM` by `kill -15`

#### Example

```php
function onShutdown(swoole_server $server)
```
