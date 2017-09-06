# Swoole Process Manager

## Methods 

### swoole_process->read

#### Prototype

```php
string swoole_process->read(int $buffer_size=8192);
```

#### Illustration

Read data from the pipe:

#### Parameter

- `$buffer_size` the size of buffer

#### Return

the string of data readed

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
