## Events and Callback functions 

### onPacket

The event `packet` happens when the worker process recevice the UDP package.

The callback function registered for event `packet` is called in the process where the event happens.

#### Example

```php
function onPacket(swoole_server $server, string $data, array $client_info)
```

- `$data` the UDP package received

- `$client_info`, this data is an array.
    ```php
    Array                                                                                         
    (                                                                                             
     [server_socket] => 4                                                                      
     [server_port] => 9501                                                                 
     [address] => 127.0.0.1                                                            
     [port] => 47306                                                               
    )    
    ```

If the swoole server listens on TCP and UDP port, the callback function `onReceive` will be called when TCP data is received and the callback function `onPacket` will be called when UDP data is received.


#### Data transformation

Transform the data to the `$fd` and `reactor_id` of callback function `onReceive`

```php
$fd = unpack('L', pack('N', ip2long($addr['address'])))[1];
$reactor_id = ($addr['server_socket'] << 16) + $addr['port'];
```
