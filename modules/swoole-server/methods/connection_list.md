## Method

### swoole_server->connection_list

#### Prototype

```php
mixed swoole_server->connection_list(int $start_fd = 0, int $pagesize = 10)
```

#### Illustration

Get the list of all the TCP connections for all the workers.

> this method is besed on the shared memory and is fast.

#### Parameter

* `$start_fd`	the start id number of client list
* `$pagesize`   the pagesize of list

#### Return

the array list of the `$fd` client 

if fail, the result is false 

#### Example

``` php
<?php
$start_fd = 0;
while(true)
{
    $conn_list = $serv->connection_list($start_fd, 10);
    if($conn_list===false or count($conn_list) === 0)
    {
        echo "finish\n";
        break;
    }
    $start_fd = end($conn_list);
    var_dump($conn_list);
    foreach($conn_list as $fd)
    {
        $serv->send($fd, "broadcast");
    }
}
```
