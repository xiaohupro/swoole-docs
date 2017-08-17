## Method

### swoole_server->reload

#### Prototype

```php
bool swoole_server->reload(bool $only_reload_taskworkrer = false)
```

#### Illustration

Gracefully restart all the worker processes and reload the PHP files.

- The reload only works for the files included after `onWorkerStart` and `onReceive`, and not for the files included before the start of the swoole_server 
- The reload not works for the runtime setting of the swoole server. The runtime setting should be changed by the restart of swoole server

#### Parameter

* `$only_reload_taskworkrer` if the call of reload only reloads taskworkrer

#### Return

the result if it has been reloaded successfully 

#### Example

Restart all the worker processes by signal

``` bash
kill -USR1 MASTER_PID
```

Only restart the task processes by signal

``` bash
kill -USR2 MASTER_PID
```

Get all the files loaded before the worker started

``` php
<?php
$server->on('WorkerStart', function($serv, $workerId) {
    var_dump(get_included_files());
});
```

When using APC/OpCache

* *stat* in APC/OpCache has to be enabled for code reload
* Refresh OpCache with apc_clear_cache() or opcache_reset() if necessary
