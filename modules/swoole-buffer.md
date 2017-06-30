# Swoole buffer

Memory management module enable developers managing memory like C language without worrying about memory allocation, release.

``` php
<?php
$buffer = new swoole_buffer();
$buffer->append(str_repeat("A", 10));
$buffer->append(str_repeat("B", 20));
$buffer->append(str_repeat("C", 30));
var_dump($buffer);
```