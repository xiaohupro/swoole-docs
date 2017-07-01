# Swoole Modules

## [Swoole Server](/modules/swoole-server.md) {#entry_h2_0}

Swoole server provides the API to write TCP / UDP / UnixSocket servers.

### [Swoole HTTP Server](/modules/swoole-http-server.md)

Swoole HTTP server provides the API to write HTTP servers.

### [Swoole WebSocket Server](/modules/swoole-websocket-server.md)

Swoole WebSocket server provides the API to write WebSocket servers.

### [Swoole Redis Server](/modules/swoole-redis-server.md)

Swoole Redis server provides the API to write TCP servers with Redis protocol.

## [Swoole TCP/UDP Client](/modules/swoole-client.md) {#entry_h2_1}

Swoole client provide the API to write TCP/UDP/UnixSocket/HTTP clients, supports IPv4/IPv6 protocol. Developers can write sync or async client side features with swoole client API.

## swoole\_event {#entry_h2_2}

Developers can use swoole event API to operate the EventLoop API.

> Currently, swoole\_event API can not be used to operate File IO.

## [Swoole Async IO](/modules/swoole-async-io.md) {#entry_h2_3}

Async API includes the async File IO API, Timer, async HTTP client API, async MySQL client API,  async Redis client API and async DNS client API.

**swoole\_timer**

**swoole\_async\_read**

**swoole\_async\_write**

## [Swoole Process Manager](/modules/swoole-process.md) {#entry_h2_4}

Linux process management module can be used to create new Linux process, manage the processes, and the communication between different processes.

## Swoole memory

### [Swoole Atomic](/modules/swoole-atomic.md) {#entry_h2_5}

Integer variable allows any processor to atomically test and modify. Implemented based on CPU atomic instructions.

### [Swoole Buffer](/modules/swoole-buffer.md) {#entry_h2_6}

Memory management module enable developers managing memory like C language without worrying about memory allocation, release.

### [Swoole Table](/modules/swoole-table.md) {#entry_h2_7}

Swoole table is a high performance memory management module, implemented based on shared memory and spin lock.

### [Swoole Mmap](/modules/swoole-mmap.md) {#entry_h2_8}

Swoole provides the api to use mmap for files access.

### [Swoole Channel](/modules/swoole-channel.md) {#entry_h2_9}

Memory data structure likes Chan in Golang, implemented based on shared memory and Mutex locks. It can be used as high performance message queue in memory. 

### [Swoole Lock](/modules/swoole-lock.md) {#entry_h2_10}

Swoole locks enable PHP developers use locks for data synchronization between multiple theads or processes.


