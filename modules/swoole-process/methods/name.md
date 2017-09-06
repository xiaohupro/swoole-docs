# Swoole Process Manager

## Methods 

### swoole_process->name

#### Prototype

```php
bool swoole_process->name(string $new_process_name);
```

#### Illustration

Set name of the process started.

#### Parameter

void

#### Return

the pid of child process, or return false if the fork is failed. You can use `swoole_errno` and `swoole_strerror` to get the code and information of error.
