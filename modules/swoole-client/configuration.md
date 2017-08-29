# Swoole TCP/UDP client

## Configuration

There are some configurations available to set the swoole client.

``` php
<?php
// Check EOF
$client->set(array(
    'open_eof_check' => true, // if check the EOF
    'package_eof' => "\r\n\r\n", // EOF
    'package_max_length' => 1024 * 1024 * 2,
));

// Check package length
$client->set(array(
    'open_length_check'     => 1,
    'package_length_type'   => 'N',
    'package_length_offset' => 0,       // The offset of package length variable
    'package_body_offset'   => 4,       // The offset of body of the package
    'package_max_length'    => 2000000,  // The max length of the package
));

// Set the socket buffer size
$client->set(array(
    'socket_buffer_size'     => 1024*1024*2, // 2MB buffer size
));

// Turn off the Nagle TCP algorithm
$client->set(array(
    'open_tcp_nodelay'     =>  true,
));

// Setup SSL files
$client->set(array(
    'ssl_cert_file'     =>  $your_ssl_cert_file_path,
    'ssl_key_file'     =>  $your_ssl_key_file_path,
));

// Setup local TCP address
$client->set(array(
    'bind_address'     =>  '192.168.1.100',
    'bind_port'     =>  36002,
));

// Setup socks5 proxy
$client->set(array(
    'socks5_host'     =>  '192.168.1.100',
    'socks5_port'     =>  1080,
    'socks5_username' => 'username',
    'socks5_password' => 'password',
));
```
