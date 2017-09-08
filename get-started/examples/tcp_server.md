## Create TCP Server

### Code example

`server.php`

``` php
// Create the server object and listen 127.0.0.1:9501 port
$server = new swoole_server("127.0.0.1", 9501);

// Register the function for the event of connecting
$server->on('connect', function($server, $fd){
    echo "Client : Connect.\n";
});

// Register the function for the event of receiving
$server->on('receive', function($server, $fd, $from_id, $data){
    $server->send($fd, "Server: " . $data);
});

// Register the function for the event of close
$server->on('close', function($server, $fd){
    echo "Client: {$fd} close.\n";
});

// Start the server
$server->start();
```
The code above creates a TCP server, and listens the 127.0.0.1:9501 port. It implements a
simple echo tcp server. When the client connect this server and send a string 'hello', the server will reply a string 'Server: hello'.

The class swoole_server creates the async server by registering the events listening functions. When the event happens, the internal of swoole will call the corresponding function which is registered. 

For example, if a tcp connection comes, the swoole will call the function which is registered for connection event. If a tcp connection send data to swoole, the swoole will recevice the data and call the corresponding function to handle this event. 

- The server can be connected by thousands of client and `$fd` is the unique identifier of client.

- When calling `$server->send($fd, $data)` to send data to client, `$fd` stands for the client.

- When calling `$server->close($fd)`, the connection with client `$fd` will be closed and the server will call the function registered for close event.

- When the client closes the connection proactively, the server will call the function registered for close event 

### Run program

``` bash
php server.php
```

Run the server file in command line. You can use the `netstat` to check which process is listening the 9501 port. 

`sudo netstat -nlp |awk '/9501/'`

Use the `telnet` or `netcat` tool to connect the server.
``` bash
telnet 127.0.0.1 9501
hello
Server: hello
```

### Q&A

#### Fail to connect the server

- Run `sudo netstat -nlp | grep 9501` to check if the 9501 has been listening

- If above checked no problem, check the firewall of os

- Pay attention to the ip address the server use. The client should connect the same ip address
