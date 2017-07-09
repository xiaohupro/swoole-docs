# Swoole Lock

Swoole locks enable PHP developers use locks for data synchronization between multiple theads or processes.

Lock types:

* SWOOLE_FILELOCK: file lock
* SWOOLE_RWLOCK: read write lock
* SWOOLE_SEM: Linux semaphore
* SWOOLE_MUTEX: Mutex
* SWOOLE_SPINLOCK: spin lock

### Methods

#### swoole_lock->__construct($type, $file_lock_location = '/tmp/file.lock');

#### swoole_lock->__destruct();

#### swoole_lock->lock();

#### swoole_lock->trylock();

#### swoole_lock->lock_read();

#### swoole_lock->trylock_read();

#### swoole_lock->unlock();

### Example:

``` php
<?php

$lock = new swoole_lock(SWOOLE_MUTEX);
echo "[Master] Create lock\n";
$lock->lock();
if (pcntl_fork() > 0)
{
    sleep(1);
    $lock->unlock();
} 
else
{
    echo "[Child] Wait Lock\n";
    $lock->lock();
    echo "[Child] Get Lock\n";
    $lock->unlock();
    exit("[Child] exit\n");
}
echo "[Master]release lock\n";
unset($lock);
sleep(1);
echo "[Master]exit\n";
```