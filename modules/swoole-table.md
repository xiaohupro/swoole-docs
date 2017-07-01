# Swoole table

Swoole table is a high performance memory management module, implemented based on shared memory and spin lock. 

> In order to keep the data synchronization, have to use Swoole\Lock if the memory is modified and accessed by multiple threads or processes.

### Why use swoole table

* High performance, the single thread read/write speed is more than 2 millions per second.
* Can be used by multiple threads or processes.

### Iterator and Countable

> The iterator and countable depends on pcre-devel

```php
<?php
foreach($table as $row)
{
    var_dump($row);
}
echo count($table);
```


