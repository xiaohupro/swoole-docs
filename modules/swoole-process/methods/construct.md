# Swoole Process Manager

## Methods 

### swoole_process->__construct

#### Prototype

```php
int swoole_process->__construct(mixed $function, $redirect_stdin_stdout = false, $create_pipe = true);
```

#### Illustration

Construct a child process with the callback function executed in the child process, optionally redirect the standard I/O to pipes between the parent process and the child processes.

> When the parent process is stopped, the child processes will receive *CLOSE* event from the pipe.

#### Parameter

- `$function` the callback function executed in the child process

- `$redirect_stdin_stdout`

- `$create_pipe`

#### Return


#### Example
