# Swoole Process Manager

## Methods 

### swoole_process->statQueue

#### Prototype

```php
array swoole_process->statQueue();
```

#### Illustration

Get the stats of the message queue used as the communication method between processes.

#### Parameter

void

#### Return

the array of message queue

```php
array(
    "queue_num" => 10, // number of task in the queue
    "queue_bytes" => 161, // the total bytes of data in the queue
);
```

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
        
        exit(0);
    }, false, false);
    
    $res = $process->useQueue(0, 2);
    
    $pid = $process->start();

    $child_processes[(string)$pid] = $process;
}

foreach($child_processes as $pid => $child_process)
{
    $child_process->push("From main process : Hello child process {$pid}\n");

    echo "the stat of queue : ";
    
    var_dump($child_process->statqueue());
}
```
