# Swoole WebSocket server

The following PHP codes shows how to write a simple WebSocket server. The WebSocket server sends the client a message when the WebSocket connection is established.

The `swoole_websocket_server` class inherits from the class `swoole_server`.

## Example Code

``` php
<?php
$server = new swoole_websocket_server("127.0.0.1", 9501);

$server->on('open', function (swoole_websocket_server $server, $request) {
    echo "server: handshake success with fd{$request->fd}\n";
});

$server->on('message', function (swoole_websocket_server $server, $frame) {
    echo "receive from {$frame->fd}:{$frame->data},opcode:{$frame->opcode},fin:{$frame->finish}\n";
    $server->push($frame->fd, "This message is from swoole websocket server.");
});

$server->on('close', function ($ser, $fd) {
    echo "client {$fd} closed\n";
});

$server->start();
```

## Table of Contents

* [Events And Callback Functions](/modules/swoole-websocket-server/events-callbacks.md)

* [Methods List](/modules/swoole-websocket-server/methods.md)

* [Predefineds Contants](/modules/swoole-websocket-server/constants.md)

* [Common Problems](/modules/swoole-websocket-server/common-problems.md)

> If the swoole_websocket_server has been setted the callback function of event `request`, it can be used as Http server.

> If the swoole_websocket_server hasn't been setted the callback function of event `request` and received http request, it would repond http 400 error.


### Events

* open
* handshake
* message
* close


### Override the default on handshake callback

There is a default on handshake callback in the Swoole WebSocket server. But developers can write custom function to override the default callback function.

``` php
<?php
function onHandShake(swoole_http_request $request, swoole_http_response $response);
```

> When the custom on handshake function is implemented, the *onOpen* callback function will not be called.

### Sample onHandShake function

``` php
<?php
$server->on('handshake',function(\swoole_http_request $request,$swoole_http_response $response){
  // End the connection
  //if(){
  //    $response->end();
  //    return false;
  //}
  // WebSocket handshake logic
  if(0===preg_match('#^[+/0-9A-Za-z]{21}[AQgw]==$#',$request->header['sec-websocket-key']) || 16!==strlen(base64_decode($request->header['sec-websocket-key']))){
    $response->end();
    return false;
  }
  $key=base64_encode(sha1($request->header['sec-websocket-key'].'258EAFA5-E914-47DA-95CA-C5AB0DC85B11',true));
  $headers=array(
    'Upgrade'=>'websocket',
    'Connection'=>'Upgrade',
    'Sec-WebSocket-Accept' =>$key,
    'Sec-WebSocket-Version'=>'13',
    'Sec-WebSocket-Protocol'=>$request->header['sec-websocket-protocol'],
  );
  foreach($headers as $key=>$val){
    $response->header($key,$val);
  }
  $response->status(101);
  $response->end();
  echo "connected!".PHP_EOL;
  return true;
});
```

### Callback functions

* onOpen
* onMessage
* onHandShake

### Methods

#### void swoole_websocket_server->on($event_name, $callback);

Register event callback functions before server started.

#### void swoole_websocket_server->push($fd, $data, $opcode = 1, $fin = true);

Push data to the connected websocket client.

#### string swoole_websocket_server->pack($data, $length = DATA_LENGTH, $opcode = 1, $finish = true, $mask = false);

Encode data.

#### string swoole_websocket_server->unpack($data);

Decode data.

#### boolean swoole_websocket_server->exist($fd);

Check if the connection to the websocket client is active.


