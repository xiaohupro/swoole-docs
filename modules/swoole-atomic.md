# Swoole Atomic

Integer variable allows any processor to atomically test and modify. Implemented based on CPU atomic instructions. 

> The Swoole atomic variables have to defined before *swoole_server->start*.

Compare-and-swap (CAS) is an atomic instruction used in multithreading to achieve synchronization. It compares the contents of a memory location with a given value and, only if they are the same, modifies the contents of that memory location to a new given value. 

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

Construct a swoole atomic object.

#### swoole_atomic->add($add_value);

Add a number to the value fo the atomic object.

#### swoole_atomic->sub($sub_value);

Subtract a number to the value of the atomic object.

#### swoole_atomic->get();

Get the current value of the atomic object.

#### swoole_atomic->set($value);

Set the value to the atomic object.

#### swoole_atomic->cmpset($value);

Compare and set the value of the atomic object. See more about [Compare and set](https://en.wikipedia.org/wiki/Compare-and-swap).