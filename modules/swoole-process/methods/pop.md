# Swoole Process Manager

## Methods 

### swoole_process->pop

#### Prototype

```php
string swoole_process->pop(int $maxsize = 8192);
```

#### Illustration

Read and pop data from the message queue.

#### Parameter

- `$maxsize` the max size of data to read from the message queue

#### Return

if failed, it returns `false`. Or it returns the data.

In the blocking mode, if the queue is empty, the call of this method will block.

In the non-blocking mode, if the queue is empty, the call of this method will return `false` immediately and set the error code to `ENOMSG`.
