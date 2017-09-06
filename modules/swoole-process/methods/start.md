# Swoole Process Manager

## Methods 

### swoole_process->start

#### Prototype

```php
int swoole_process->start();
```

#### Illustration

Fork the swoole child process constructed and return the *PID* of the child process, or return false if the fork is failed. 

Attributes of the child process:

``` php
<?php
$process->pid  // the pid of child process
$process->pipe // the file descriptor of pipe
```

#### Parameter

void

#### Return

the pid of child process, or return false if the fork is failed. You can use `swoole_errno` and `swoole_strerror` to get the code and information of error.

#### Example
```
<?php
$workers = [];
$worker_num = 3;

for($i=0;$i<$worker_num ; $i++){
    
    $process = new swoole_process('process');
    $pid = $process->start();
    $workers[$pid] = $process;

    echo "create a child process\n";
}

foreach($workers as $process)
{
    swoole_event_add($process->pipe, function ($pipe) use($process){
        $data = $process->read();
        echo "RECV: " . $data . "\n";
    });
}

function process(swoole_process $process){
    sleep(rand(5, 10)); 
    $process->write($process->pid);
    echo $process->pid . "\n";
}
```
