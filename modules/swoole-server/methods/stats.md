## Method

### swoole_server->stats

#### Prototype

```php
array swoole_server->stats()
```

#### Illustration

Get the TCP connections stats of the current server.

#### Parameter

void

#### Return

the array of connections stats of the current server

``` php
<?php
array (
  'start_time' => 1409831644,  // the time of server since start
  'connection_num' => 1,       // the number of current connections 
  'accept_count' => 1,         // the number of connections accepted
  'close_count' => 0,          // the number of connections closed
  'tasking_num' => 1,          // the number of task which is queuing up
  'request_count' => 11,       // the number of request received
  'worker_request_count'       // the number of request received by the current worker
  'task_queue_num' => 10,      // the number of task which is in queue of task
  'task_queue_bytes' => 65536, // the number of bytes which is the space occupied by the queue of task
);
```

#### Example
