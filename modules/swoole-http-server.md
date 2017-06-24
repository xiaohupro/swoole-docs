# Swoole HTTP server

With 5 lines of code, you can write an Async non-blocking IO, multiple process HTTP server.

``` php
$http = new swoole_http_server("127.0.0.1", 9501);

$http->on('request', function ($request, $response) {

    $response->end("<h1>Hello World. #".rand(1000, 9999)."</h1>");

});

$http->start();
```

> swoole_http_server does not support the complete HTTP protocol, Nginx is recommended to be used as a proxy for Swoole HTTP server.

### Performance

Compare with PHP-FPM, the default Golang HTTP server, the default Node.js HTTP server, Swoole HTTP server performs much better. It has the similar performance compare with the Nginx static files server. 

The experiment is done with benchmark tool Apache bench, on a normal PC server with Inter Core-I5 4 core CPU, 8GB memory. The QPS reaches 110K.

