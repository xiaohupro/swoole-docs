# Swoole memory management

Swoole provides 6 different memory operation APIs: Lock, Buffer, Table, Atomic, MMap, Channel which can be used when developing multiple process programs.

All these API are async and non-blocking, multiple-process safe. Don't have to warry about the data sync issues. 

### [Swoole Lock](/modules/swoole-lock.md) {#entry_h2_1}

Swoole locks enable PHP developers use locks for data synchronization between multiple theads or processes.

### [Swoole Atomic](/modules/swoole-atomic.md) {#entry_h2_5}

Integer variable allows any processor to atomically test and modify. Implemented based on CPU atomic instructions.

### [Swoole Buffer](/modules/swoole-buffer.md) {#entry_h2_6}

Memory management module enable developers managing memory like C language without worrying about memory allocation, release.

### [Swoole Table](/modules/swoole-table.md) {#entry_h2_7}

Swoole table is a high performance memory management module, implemented based on shared memory and spin lock.

### [Swoole MMap](/modules/swoole-mmap.md) {#entry_h2_8}

Swoole provides the api to use mmap for files access.

### [Swoole Channel](/modules/swoole-channel.md) {#entry_h2_9}

Memory data structure likes Chan in Golang, implemented based on shared memory and Mutex locks. It can be used as high performance message queue in memory. 


