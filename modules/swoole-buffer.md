# Swoole Buffer

Memory management module enable developers managing memory like C language without worrying about memory allocation and release.

> The memory allocated by swoole_buffer is not shared memory and can not be accessed by multiple processes.

### Quick Example

``` php
<?php
$buffer = new swoole_buffer();
$buffer->append(str_repeat("A", 10));
$buffer->append(str_repeat("B", 20));
$buffer->append(str_repeat("C", 30));
var_dump($buffer);
```

### Methods

#### swoole_buffer->__construct(int $size = 128);

Fixed size memory blocks allocation.

#### int swoole_buffer->append(string $data);

Append the string or binary data at the end of the memory buffer and return the new size of memory allocated.

#### string swoole_buffer->substr(int $offset, int $length = -1, bool $remove = false);

Read data from the memory buffer based on offset and length. Or remove data from the memory buffer.

> If $remove is set to be true and $offset is set to be 0, the data will be removed from the buffer. The memory for storing the data will be released when the buffer object is deconstructed.

#### swoole_buffer->clear();

The memory buffer will be reset.

#### swoole_buffer->expand(int $new_size);

Expand the size of memory buffer.

#### swoole_buffer->write(int $offset, string $data);

Write data to the memory buffer. The memory allocated for the buffer will not be changed.

#### swoole_buffer->read(int $offset, int $length)

Read data from the memory buffer based on offset and length.

#### swoole_buffer->recycle();

Release the memory to OS which is not used by the memory buffer.



