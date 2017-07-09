# Swoole MMap

Swoole provides the api to use mmap for files access. This is useful when multiple threads or processes accessing data in a read only fashion from the same file.

### Example

``` php
<?php
$file = __DIR__.'/data.dat';
$size = 8192;
if (!is_file($file)) {
    file_put_contents($file, str_repeat("\0", $size));
}

$fp = swoole\mmap::open($file, 8192);

fwrite($fp, "hello world\n");
fwrite($fp, "hello swoole\n");

fflush($fp);
fclose($fp);
```

### Methods

#### function swoole_mmap->open($file, $size = -1, $offset = 0);

Map a file into memory and return a *stream* resource which can be used by PHP stream operations.

### Methods to use mmap in PHP

* *fread*: read data from mmap stream
* *fgets*: read data from mmap stream
* *fwrite*: write data to mmap stream
* *fputs*: write data to mmap stream
* *fflush*: sync data on the disk file
* *fclose*: sync data on the disk file and close the file

