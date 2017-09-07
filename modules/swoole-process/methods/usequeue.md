# Swoole Process Manager

## Methods 

### swoole_process->useQueue

#### Prototype

```php
bool swoole_process->useQueue(int $msgkey = 0, int $mode = 2);
```

#### Illustration

Create a message queue as the communication method between the parent process and child processes.

> It can't use the pipe and message queue the same time.

> Before the start of the swoole process, it can also call the method `push` and `pop`

#### Parameter

- `$msgkey` the ID of the message queue, the default value is *ftok(__FILE__, 1)*

- `$mode` `2` : competitive mode, all the processes created will compete for the message received by the message queue.
                Set the mode to `$mode | swoole_process::IPC_NOWAIT` to make the message queue non-blocking. In the non-blocking mode, it will return immediately when the method `push` is called in the condition of full queue and the method `pop` is called in the condition of empty queue.

#### Return

bool

#### Example
```
<?php
$child_num = 3;
$child_processes = [];
for($i = 1; $i <= $child_num; $i++)
{
    $process = new swoole_process(function($worker){
        echo "the pid of child process is " . $worker->pid . "\n";
        
        $worker->name("php child process");
        
        $recv = $worker->pop();
        
        echo "To child process " . $worker->pid .  " : " . $recv;

        echo "the child process " . $worker->pid . " exited\n";
        
        exit(0);
    }, false, false);
    
    $res = $process->useQueue(0, 2);
    
    $pid = $process->start();

    $child_processes[(string)$pid] = $process;
}

foreach($child_processes as $pid => $child_process)
{
    $child_process->push("From main process : Hello child process {$pid}\n");
}
```
