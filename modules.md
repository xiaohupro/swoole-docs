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

## [Swoole Process Manager](/modules/swoole-process.md) {#entry_h2_2}

Linux process management module can be used to create new Linux process, manage the processes, and the communication between different processes.

## [Swoole Async File I/O](/modules/swoole-async-io.md) {#entry_h2_3}

Async API includes the async File IO API, Timer, async HTTP client API, async MySQL client API,  async Redis client API and async DNS client API.

## [Swoole MySQL Client](/modules/swoole-async-mysql-client.md) {#entry_h2_4}

The swoole async MySQL client is a replacement of the other sync MySQL clients: libmysqlclient, mysqlnd, mysqli.

## [Swoole Redis Client](/modules/swoole-async-redis-client.md) {#entry_h2_5}

Swoole async redis client is based on *hiredis*.

## [Swoole Async Http/WebSocket Client](/modules/swoole-async-http-client.md) {#entry_h2_6}

Swoole Async HTTP client is a high performance and aync HTTP client supports Http-Chun, Keep-Alive, form-data.

## [Swoole Async Http2 Client](/modules/swoole-async-http2-client.md) {#entry_h2_7}

Http2.0 client support stream and multiplexing. Multiple GET or POST request can be sent over the same TCP connection.

## [Swoole EventLoop](/modules/swoole-event-loop.md) {#entry_h2_8}

Developers can use swoole EventLoop API to use the system EventLoop.

## [Swoole Scheduler](/modules/swoole-scheduler.md) {#entry_h2_8}

Schedule functions to run at set intervals, accurate to milliseconds.

## [Swoole Serialize](/modules/swoole-serialize.md) {#entry_h2_8}

Schedule functions to run at set intervals, accurate to milliseconds.

## Swoole Memory Management

### [Swoole Atomic](/modules/swoole-atomic.md) {#entry_h2_9}

Integer variable allows any processor to atomically test and modify. Implemented based on CPU atomic instructions.

### [Swoole Buffer](/modules/swoole-buffer.md) {#entry_h2_10}

Memory management module enable developers managing memory like C language without worrying about memory allocation, release.

### [Swoole Table](/modules/swoole-table.md) {#entry_h2_11}

Swoole table is a high performance memory management module, implemented based on shared memory and spin lock.

### [Swoole MMap](/modules/swoole-mmap.md) {#entry_h2_12}

Swoole provides the api to use mmap for files access.

### [Swoole Channel](/modules/swoole-channel.md) {#entry_h2_13}

Memory data structure likes Chan in Golang, implemented based on shared memory and Mutex locks. It can be used as high performance message queue in memory. 

### [Swoole Lock](/modules/swoole-lock.md) {#entry_h2_14}

Swoole locks enable PHP developers use locks for data synchronization between multiple theads or processes.


