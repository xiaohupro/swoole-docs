# Swoole Modules

## [swoole\_server](/modules/swoole-server.md) {#entry_h2_0}

Swoole server provide the API to write TCP/UDP/UnixSocket/HTTP/WebSocket servers.

### [swoole\_http\_server](/modules/swoole-http-server.md)

### [swoole\_websocket\_server](/modules/swoole-websocket-server.md)

### [swoole\_redis\_server](/modules/swoole-redis-server.md)

## [swoole\_client](/modules/swoole-client.md) {#entry_h2_1}

Swoole client provide the API to write TCP/UDP/UnixSocket/HTTP clients, supports IPv4/IPv6 protocol. Developers can write sync or async client side features with swoole client API.

## swoole\_event {#entry_h2_2}

Developers can use swoole event API to operate the EventLoop API.

> Currently, swoole\_event API can not be used to operate File IO.

## [swoole\_async](/modules/swoole-async-io.md) {#entry_h2_3}

Async API includes the async File IO API, Timer, async HTTP client API, async MySQL client API,  async Redis client API and async DNS client API.

**swoole\_timer**

**swoole\_async\_read**

**swoole\_async\_write**

## [swoole\_process](/modules/swoole-process.md) {#entry_h2_4}

Linux process management module can be used to create new Linux process, manage the processes, and the communication between different processes.

## swoole\_buffer {#entry_h2_5}

Memory management module enable developers managing memory like C language without worrying about memory allocation, release.

## swoole\_table {#entry_h2_6}

Based on shared memory and spin lock, swoole table is a high performance memory management module.

