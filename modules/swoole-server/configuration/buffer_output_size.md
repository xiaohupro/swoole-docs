## Configuration

### buffer_output_size

Set the output buffer size in the memory.

The default value is 2M. The data to send can't be larger than `buffer_output_size` every times.

#### Usage
```php
$server->set([
    'buffer_output_size' => 32 * 1024 *1024, // byte in unit
])
```


