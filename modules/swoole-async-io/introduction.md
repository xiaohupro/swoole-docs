# Swoole Async File I/O

The task process in swoole_server is syncing and blocking without using EventLoop, can't benefit from Async I/O.

### Events

NA

### Methods

#### swoole_async_set(array $setting);

Update the Async I/O options:

* thread_num: number of async file I/O threads
* aio_mode: AIO mode: SWOOLE_AIO_BASE/SWOOLE_AIO_LINUX
* enable_signalfd: whether enable signalfd
* socket_buffer_size: socket buffer size
* socket_dontwait: do not block when the buffer is full

#### swoole_async_readfile(string $filename, mixed $callback);

Read files in the async way.

Example:

``` php
<?php
swoole_async_readfile(__DIR__."/server.php", function($filename, $content) {
     echo "$filename: $content";
});
```

#### swoole_async_writefile(string $filename, string $fileContent, callable $callback = null, int $flags = 0)

Write file in the async way.

Example:

``` php
<?php
swoole_async_writefile('test.log', $file_content, function($filename) {
    echo "wirte ok.\n";
}, $flags = 0);
```

#### bool swoole_async_read(string $filename, mixed $callback, int $size = 8192, int $offset = 0);

Read the file content stream in the async way. When the operation of reading content from file finished, the callback registered is callback automatically.

The difference between this method and `swoole_async_readfile` is that the former reads file by fragment and uses less memory. This method reads content of `$size` length from file every time and can be used to read big file.

#### bool swoole_async_write(string $filename, string $content, int $offset = -1, mixed $callback = NULL);

Write file stream in the async way. When the operation of writing content to file finished, the callback registered is callback automatically.

The difference between this method and `swoole_async_writefile` is that the former writes file by fragment and uses less memory.

- `$offset` The method uses the `$offset` parameter to decide the postion to write file. 
            If the `$offset` is setted to `-1`, it stands for that it appends content to the end of file.
            If the aio mode setted by `swoole_async_set` is `SWOOLE_AIO_BASE`, the method can't support append content to the end of file and must set the value of `$content` and `$offset` to integer multiples of 512. Otherwise the call of this method will fail and set the error code to `EINVAL`.

#### swoole_async_dns_lookup(string $host, mixed $callback)

Async DNS lookup. The call of this method is non-blocking. 

- If the operation of DNS lookup finished, the callback registered is called automatically.

- If the operation of DNS lookup failed, the callback registered is also called automatically and the parameter `$ip` will be empty.

Example:

``` php
<?php
// Disable DNS cache
swoole_async_set(array(
    'disable_dns_cache' => true,
));
// Set the DNS server list
swoole_async_set(array(
    'dns_server' => '8.8.8.8',
));
// Lookup using random DNS server
swoole_async_set(array(
    'dns_lookup_random' => true,
));

// Lookup the DNS of www.google.com
swoole_async_dns_lookup("www.google.com", function($host, $ip){
    echo "{$host} : {$ip}\n";
});
echo "start async dns lookup\n";
```
