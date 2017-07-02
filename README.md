# Swoole Docs

Swoole is an high-performance network communication framework uses an event-driven, asynchronous, non-blocking I/O model makes it scalable and efficient. It is written in C language without 3rd party libraries.

It enables PHP developers write high performance, scalable, concurrent TCP, UDP, Unix Socket, HTTP, WebSocket services with PHP programming language without  too much knowledge about non-blocking I/O programming and low level Linux kernel.

Compare with other Async programming framework or software such as Nginx, Tornado, Node.js, Swoole has the built-in async, multiple thread I/O modules. Developers can use sync or async API to write the applications.

Swoole PHP network framework enhances the efficiency of R&D team, enable them focus on the development of innovative products.

**Features:**

* Asynchronous PHP programming
* Async TCP/UDP/HTTP/WebSocket/HTTP2 server side API
* Async TCP/UDP client side API
* Async MySQL client API and thread pool
* Async Redis client API
* Async DNS client API
* Message Queue API
* Async Task API
* Millisecond scheduler
* Async File I/O API

**Use cases:**

* Web applications and systems
* Mobile communication systems
* Online game systems
* Internet of Things
* Car networking 
* Smart home systems

Swoole framework is open source and free. Released under the license of Apache 2.0.

### [Get started](get-started.md)

#### [Installation](/get-started/installation.md) {#entry_h2_0}

### Swoole Modules

#### [Swoole Server](/modules/swoole-server.md) {#entry_h2_0}

Swoole server provides the API to write TCP / UDP / UnixSocket servers.

#### [Swoole HTTP Server](/modules/swoole-http-server.md)

Swoole HTTP server provides the API to write HTTP servers.

#### [Swoole WebSocket Server](/modules/swoole-websocket-server.md)

Swoole WebSocket server provides the API to write WebSocket servers.

#### [Swoole Redis Server](/modules/swoole-redis-server.md)

Swoole Redis server provides the API to write TCP servers with Redis protocol.

#### [Swoole TCP/UDP Client](/modules/swoole-client.md) {#entry_h2_1}

Swoole client provide the API to write TCP/UDP/UnixSocket/HTTP clients, supports IPv4/IPv6 protocol. Developers can write sync or async client side features with swoole client API.

#### [Swoole Process Manager](/modules/swoole-process.md) {#entry_h2_2}

Linux process management module can be used to create new Linux process, manage the processes, and the communication between different processes.

#### [Swoole Async File I/O](/modules/swoole-async-io.md) {#entry_h2_3}

Async API includes the async File IO API, Timer, async HTTP client API, async MySQL client API,  async Redis client API and async DNS client API.

#### [Swoole MySQL Client](/modules/swoole-async-mysql-client.md) {#entry_h2_4}

The swoole async MySQL client is a replacement of the other sync MySQL clients: libmysqlclient, mysqlnd, mysqli.

#### [Swoole Redis Client](/modules/swoole-async-redis-client.md) {#entry_h2_5}

Swoole async redis client is based on *hiredis*.

#### [Swoole Async Http/WebSocket Client](/modules/swoole-async-http-client.md) {#entry_h2_6}

Swoole Async HTTP client is a high performance and aync HTTP client supports Http-Chun, Keep-Alive, form-data.

#### [Swoole Async Http2 Client](/modules/swoole-async-http2-client.md) {#entry_h2_7}

Http2.0 client support stream and multiplexing. Multiple GET or POST request can be sent over the same TCP connection.

#### [Swoole EventLoop](/modules/swoole-event-loop.md) {#entry_h2_8}

Developers can use swoole EventLoop API to use the system EventLoop.

#### Swoole Memory Management

#### [Swoole Atomic](/modules/swoole-atomic.md) {#entry_h2_9}

Integer variable allows any processor to atomically test and modify. Implemented based on CPU atomic instructions.

#### [Swoole Buffer](/modules/swoole-buffer.md) {#entry_h2_10}

Memory management module enable developers managing memory like C language without worrying about memory allocation, release.

#### [Swoole Table](/modules/swoole-table.md) {#entry_h2_11}

Swoole table is a high performance memory management module, implemented based on shared memory and spin lock.

#### [Swoole Mmap](/modules/swoole-mmap.md) {#entry_h2_12}

Swoole provides the api to use mmap for files access.

#### [Swoole Channel](/modules/swoole-channel.md) {#entry_h2_13}

Memory data structure likes Chan in Golang, implemented based on shared memory and Mutex locks. It can be used as high performance message queue in memory. 

#### [Swoole Lock](/modules/swoole-lock.md) {#entry_h2_14}

Swoole locks enable PHP developers use locks for data synchronization between multiple theads or processes.



