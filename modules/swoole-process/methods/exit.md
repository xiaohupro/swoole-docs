# Swoole Process Manager

## Methods 

### swoole_process->exit

#### Prototype

```php
int swoole_process->exit(int $status=0);
```

#### Illustration

Stop the child process.

#### Parameter

- `$status` the exit status code of process. If this code is `0`, it stands for that the process exits normally and continue to execute the registered shutdown function. If this code isn't `0`, it stands for that the process exits unexpectedly and stops immediately. The father process can use `swoole_process::wait` to get the exit event and code from the child process.

#### Return

int

#### Example
```php
<?php
$child_num = 3;
$child_processes = [];
for($i = 1; $i <= $child_num; $i++)
{
    $process = new swoole_process(function($worker){
        echo "the pid of child process is " . $worker->pid . "\n";
        
        $worker->name("php child process");
        
        sleep(rand(2, 6));
        
        $worker->exit(rand(1, 255));
    }, false, false);
    
    $res = $process->useQueue(0, 2);
    
    $pid = $process->start();

    $child_processes[(string)$pid] = $process;
}

foreach($child_processes as $child_process)
{
    $ret = swoole_process::wait();
    var_dump($ret);
}
```
