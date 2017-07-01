# Swoole atomic

Integer variable allows any processor to atomically test and modify. Implemented based on CPU atomic instructions. 

> The Swoole atomic variables have to defined before *swoole_server->start*.

### Example

``` php
<?php
$atomic = new swoole_atomic(123);
echo $atomic->add(12)."\n";
echo $atomic->sub(11)."\n";
echo $atomic->cmpset(122, 999)."\n";
echo $atomic->cmpset(124, 999)."\n";
echo $atomic->get()."\n";
```