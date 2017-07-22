# Swoole HTTP server

With 5 lines of code, you can write an Async non-blocking IO, multiple process HTTP server.

### Events

* request
* handshake

### Example

``` php
<?php 
$http = new swoole_http_server("127.0.0.1", 9501);

$http->on('request', function ($request, $response) {

    $response->end("<h1>Hello World. #".rand(1000, 9999)."</h1>");

});

$http->start();
```

> swoole_http_server does not support the complete HTTP protocol, Nginx is recommended to be used as a proxy for Swoole HTTP server.

### Performance

Compare with PHP-FPM, the default Golang HTTP server, the default Node.js HTTP server, Swoole HTTP server performs much better. It has the similar performance compare with the Nginx static files server. 

The experiment is done with benchmark tool Apache bench, on a normal PC server with Inter Core-I5 4 core CPU, 8GB memory. Swoole HTTP server hits 110K request per second.

``` bash
ab -c 200 -n 200000 -k http://127.0.0.1:9501
```
### HTTP2 protocol support

Swoole HTTP server supports HTTP2 protocol thanks to *nghttp2* library. Openssl is required for HTTP2 protocol and the openssl has to support TLS1.2, ALPN and NPN. 

PHP extension compile configuration:

``` bash
./configure --enable-openssl --enable-http2
```

Swoole HTTP server configuration:

``` bash
// Enable SSL
$server = new swoole_http_server("127.0.0.1", 9501, SWOOLE_PROCESS, SWOOLE_SOCK_TCP | SWOOLE_SSL);
// setup the location of ssl cert files and key files
$server->set([
    'ssl_cert_file' => $ssl_dir . '/ssl.crt',
    'ssl_key_file' => $ssl_dir . '/ssl.key',
    'open_http2_protocol' => true, // Enable HTTP2 protocol
]);
```

Nginx configuration:

``` text
server {
    root /data/wwwroot/;
    server_name localhost;

    location / {
        proxy_http_version 1.1;
        proxy_set_header Connection "keep-alive";
        proxy_set_header X-Real-IP $remote_addr;
        if (!-e $request_filename) {
             proxy_pass http://127.0.0.1:9501;
        }
    }
}
```

### Methods

#### swoole_http_server->on(string $event, $callback);

Callback functions can be registered on events:

* request : HTTP request
* handshake : HTTP2 handshake

#### swoole_http_server->start();

Start the Swoole HTTP server.

#### swoole_http_request->rawcontent();

Get the raw HTTP request content.

#### swoole_http_response->write($data);

Send data for the HTTP request.

#### swoole_http_response->end($data);

Send data for the HTTP request and end the response.

#### swoole_http_response->sendfile($file_location, $offset, $length);

Response the file content to the client.

#### swoole_http_response->cookie($name, $value, $expires, $path, $domain, $secure, $httponly);

Send cookie to the client.

#### swoole_http_response->rawcookie($name, $value, $expires, $path, $domain, $secure, $httponly);

Send raw cookie to the client.

#### swoole_http_response->header($key, $value, $ucwords = 1);

Send HTTP headers to the client.

#### swoole_http_response->initHeader();

Start the set the HTTP headers.

#### swoole_http_response->gzip($level = 1);

Whether to enable Gzip compression for the response.

#### swoole_http_response->status($status = 200);

Send the HTTP response code.

HTTP status code: [http://pages.cs.wisc.edu/~cao/http1.1-rfc2068.html](http://pages.cs.wisc.edu/~cao/http1.1-rfc2068.html)