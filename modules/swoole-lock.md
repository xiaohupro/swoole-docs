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

Construct a lock.

#### swoole_lock->__destruct();

Destory a lock.

#### swoole_lock->lock();

Try to acquire the lock. It will block if the lock is not available.

#### swoole_lock->lockwait($timeout = 1);

Try to acquire the lock and waiting the lock for a duration before giving up.

#### swoole_lock->trylock();

Try to acquire the lock and return straight away even the lock is not available.

#### swoole_lock->lock_read();

Lock a read-write lock for reading.

#### swoole_lock->trylock_read();

Try to lock a read-write lock for reading and return straight away even the lock is not available.

#### swoole_lock->unlock();

Release the lock.

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