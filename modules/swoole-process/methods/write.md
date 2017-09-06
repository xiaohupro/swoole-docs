# Swoole Process Manager

## Methods 

### swoole_process->write

#### Prototype

```php
int swoole_process->write(string $data);
```

#### Illustration

Write data into the pipe and communicate with the parent process or child processes.

#### Parameter

- `$data` the string of data to communicate

#### Return

int the length of data sent

#### Example
```php
<?php
$process = new swoole_process(function($worker){
    echo "the pid of child process is " . $worker->pid . "\n";
    echo "the file descriptor of pipe is " . $worker->pipe . "\n";
    
    $res = $worker->write("Hello main process\n");
    var_dump(strlen("Hello main process\n"));
    var_dump($res);
    
    $worker->name("php child process");
}, false, 2);

$process->start();

usleep(100);

echo $process->read();
```
