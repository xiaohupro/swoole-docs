# Swoole Process Manager

## Methods 

### swoole_process->useQueue

#### Prototype

```php
bool swoole_process->useQueue(int $msgkey = 0, int $mode = 2);
```

#### Illustration

Create a message queue as the communication method between the parent process and child processes.

#### Parameter

- `$msgkey` the ID of the message queue, the default value is *ftok(__FILE__, 1)*

- `$mode` `2` : competitive mode

#### Return

bool
