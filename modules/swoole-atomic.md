# Swoole Atomic

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

### Methods

#### swoole_atomic->__construct();

#### swoole_atomic->add($add_value);

#### swoole_atomic->sub($sub_value);

#### swoole_atomic->get();

#### swoole_atomic->set($value);

#### swoole_atomic->cmpset($value);