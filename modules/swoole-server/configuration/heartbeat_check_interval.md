## Configuration

### heartbeat_check_interval

This configuration `heartbeat_check_interval` is the interval of polling every TCP connection. 

If the connection hasn't sent any data to the server in the last interval of `heartbeat_check_interval`, the connection will be closed.

The swoole server would not send the heartbeat packet to the client but only wait for the heartbeat packet from the client. The heartbeat check of swoole server only check the last time of sending data from the client. If the time exceeds `heartbeat_check_interval`, the connection between the server and the client will be closed.
