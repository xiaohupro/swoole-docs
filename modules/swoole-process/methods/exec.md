# Swoole Process Manager

## Methods 

### swoole_process->exec

#### Prototype

```php
bool swoole_process->exec(string $execfile, array $args)
```

#### Illustration

Execute system commands:

The process will be replaced to be the system command process, but the pipe between the parent process will be kept.

If it needs to communication between the main process and child process, it must enable the redirection of stdin and stdout of child process.

#### Parameter

- `$execfile` the absolute path of the command

- `$args` the array of arguments for the command

#### Return

bool

#### Example
```php
<?php
// main process
$process = new swoole_process(function($process){
    //execute the external program
    $process->exec("/usr/bin/php", array('/code/swoole/process/testexec.php'));
}, true); // enable the redirection of stdin and stdout

$process->start();

//Inter-Process Communication Of main process and child process by stdin and stdout

$process->write("hello child process from main process");

$res = $process->read();

var_dump($res);

```
```php
<?php
// /code/swoole/process/testexec.php 
$fd = fopen('php://stdin', 'r');
$res = fread($fd, 123);
echo "the message from main process" . $res;
```
