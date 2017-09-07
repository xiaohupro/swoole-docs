# Swoole Process Manager

## Methods 

### swoole_process->push

#### Prototype

```php
bool swoole_process->push(string $data);
```

#### Illustration

Write and push data into the message queue.

#### Parameter

- `$data` the data to push to the queue, the default value is 8192 Bytes and the max value is 65536 Bytes.

#### Return

if failed, it returns `false`. Or it returns `true`.

In the blocking mode, if the queue is full, the call of this method will block.

In the non-blocking mode, if the queue is full, the call of this method will return `false` immediately.

#### Example
``` php
<?php

$workers = [];
$worker_num = 2;

for($i = 0; $i < $worker_num; $i++)
{
    $process = new swoole_process('callback_function', false, false);
    $process->useQueue();
    $pid = $process->start();
    $workers[$pid] = $process;
}

function callback_function(swoole_process $worker)
{
    echo "Child process started, PID=".$worker->pid."\n";
    //recv data from the parent process
    $recv = $worker->pop();
    echo "Data received from the parent process: $recv\n";
    sleep(2);
    $worker->exit(0);
}

foreach($workers as $pid => $process)
{
    $process->push("hello child process [$pid]\n");
}

for($i = 0; $i < $worker_num; $i++)
{
    $ret = swoole_process::wait();
    $pid = $ret['pid'];
    unset($workers[$pid]);
    echo "Child process exit, PID=".$pid.PHP_EOL;
}
```
