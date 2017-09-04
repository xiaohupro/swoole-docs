# Swoole TCP/UDP client

## Methods 

### swoole_client->wakeup

#### Prototype

```php
swoole_client->wakeup();
```

#### Illustration

Add the TCP client into the system event loop.

#### Parameter

void

#### Return

void

#### Example
``` php
$client->on("receive", function(swoole_client $cli, $data){
    //sleep mode and stop receive data
    $cli->sleep();
    swoole_timer_after(5000, function() use ($cli) {
        // wakeup the client and start to receive data
        $cli->wakeup();
    });
});
```
