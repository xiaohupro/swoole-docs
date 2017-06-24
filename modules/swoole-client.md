# Swoole client

Swoole client provide the wrapper of TCP/UDP sockets client side API. 

Compare with PHP *stream* functions, *swoole_client* is more advanced:

* There is a bug in stream function, 
* fread has the limitation length of 8129, can't support big UDP packet
* swoole_client supports waitall, able to read all the data if the packet length is known.
* swoole_client supports UDP connect, there will be no UDP packets mixing up issues.
* swoole_client has better performance.
* swoole_client supports async non-blocking callback, along with sync blocking and select API.


