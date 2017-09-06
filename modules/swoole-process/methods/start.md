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
$process->pid
$process->pipe
```

#### Parameter

void

#### Return

the pid of child process, or return false if the fork is failed. You can use `swoole_errno` and `swoole_strerror` to get the code and information of error.
