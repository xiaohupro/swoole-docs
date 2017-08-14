## Method

### swoole_server->shutdown

#### Prototype

```php
void swoole_server->shutdown()
```

#### Illustration

Shutdown the master server process, this function can be called in worker processes.

Shutdown server by system signal *SIGTERM*

``` bash
kill -15 MASTER_PID
```

#### Parameter

void

#### Return

void

#### Example
