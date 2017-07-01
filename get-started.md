# Get started

Swoole framework is released as a PHP extension \(PECL\) and run as a PHP CLI application.

### Installation

Please check the [Swoole installation guide](/get-started/installation.md).

### Hello world

An example of a web server written with Swoole which responds with 'Hello World':

``` php
<?php
$http = new swoole_http_server("127.0.0.1", 9501);

$http->on('start', function ($server) {
    echo "Swoole http server is started at http://127.0.0.1:9501\n";
});

$http->on('request', function ($request, $response) {
    $response->header("Content-Type", "text/plain");
    $response->end("Hello World\n");
});

$http->start();
```

To run the server, put the code into a file called server.php and execute it with php cli:

``` bash
$ php server.php
$ open http://127.0.0.1:9501/
```

###



