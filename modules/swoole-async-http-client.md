# Swoole Async HTTP/Websocket client

Swoole Async HTTP client is a high performance and aync HTTP client supports Http-Chun, Keep-Alive, form-data.

### Events

### Methods

#### swoole_http_client->__construct(string $host, int port, bool $ssl = false);

Example:

``` php
<?php
Swoole\Async::dnsLookup("www.google.com", function ($domainName, $ip) {
    $cli = new swoole_http_client($ip, 80);
    $cli->setHeaders([
        'Host' => $domainName,
        "User-Agent" => 'Chrome/49.0.2587.3',
        'Accept' => 'text/html,application/xhtml+xml,application/xml',
        'Accept-Encoding' => 'gzip',
    ]);
    $cli->get('/index.html', function ($cli) {
        echo "Length: " . strlen($cli->body) . "\n";
        echo $cli->body;
    });
});
```

#### swoole_http_client->set()

Set the parameters for the http client.

Example:

``` php
<?php
// Set the connect timeout
$http->set(['timeout' => 3.0]);
// Set the keep alive option
$http->set(['keep_alive' => false]);
// Set websocket mask
$http->set(['websocket_mask' => true]);
```

#### function swoole_http_client->setMethod(string $method);

Set the http request method.

Example:

``` php
<?php
$client->setMethod("PUT");
```

#### function swoole_http_client->setHeaders(array $headers);

Set the http request headers.

#### function swoole_http_client->setCookies(array $cookies);

Set the http request cookies.

#### function swoole_http_client->setData(string $data);

Set the http request body data. The http method will be changed to be *POST*.

#### function swoole_http_client->addFile(string $path, string $name, string $filename = null, string $mimeType = null, int $offset = 0, int $length)

Add files to the post form.

Example:

``` php
<?php

<?php
$cli = new swoole_http_client('127.0.0.1', 80);
//post request
$cli->setHeaders(['User-Agent' => "swoole"]);
$cli->addFile(__DIR__.'/post.data', 'post');
$cli->addFile(dirname(__DIR__).'/test.jpg', 'debug');
$cli->post('/dump2.php', array("xxx" => 'abc', 'x2' => 'rango'), function ($cli) {
    echo $cli->body;
});
```

#### function swoole_http_client->get(string $path, callable $callback);

Send *GET* http request to the remote server.

Example:

``` php
<?php

$cli = new swoole_http_client('127.0.0.1', 80);

$cli->setHeaders([
    'Host' => "localhost",
    "User-Agent" => 'Chrome/49.0.2587.3',
    'Accept' => 'text/html,application/xhtml+xml,application/xml',
    'Accept-Encoding' => 'gzip',
]);

$cli->get('/index.php', function ($cli) {
    echo "Length: " . strlen($cli->body) . "\n";
    echo $cli->body;
});
```

#### function swoole_http_client->post(string $path, mixed $data, callable $callback);

Send *POST* http request to the remote server.

Example:

``` php
<?php

$cli = new swoole_http_client('127.0.0.1', 80); 
$cli->post('/post.php', array("a" => '1234', 'b' => '456'), function ($cli) {
    echo "Length: " . strlen($cli->body) . "\n";
    echo $cli->body;
});
```

#### function swoole_http_client->upgrade(string $path, callable $callback);

Upgrade to websocket protocol.

``` php
<?php
$cli = new swoole_http_client('127.0.0.1', 9501);

$cli->on('message', function ($_cli, $frame) {
    var_dump($frame);
});

$cli->upgrade('/', function ($cli) {
    echo $cli->body;
    $cli->push("hello world");
});
// Websocket callback function
function onMessage(swoole_http_client $client, swoole_websocket_frame $frame);
```

#### function swoole_http_client->execute(string $path, callable $callback);

Send the http request after setup the parameters.

#### function swoole_http_client->download(string $path, string $filename, callable $callback, int $offset = 0);

Download file from the remote server.

Example:

``` php
<?php

$cli = new swoole_http_client('127.0.0.1', 80);

$cli->setHeaders([
    'Host' => "localhost",
    "User-Agent" => 'Chrome/49.0.2587.3',
    'Accept' => '*',
    'Accept-Encoding' => 'gzip',
]);

$cli->download('/video.avi', __DIR__.'/video.avi', function ($cli) {
    var_dump($cli->downloadFile);
});

// download by range
$cli = new swoole_http_client('127.0.0.1', 80);
$file = __DIR__.'/video.avi';
$offset = filesize($file);
$cli->setHeaders([
    'Host' => "localhost",
    "User-Agent" => 'Chrome/49.0.2587.3',
    'Accept' => '*',
    'Accept-Encoding' => 'gzip',
    'Range' => "bytes=$offset-",
]);

$cli->download('/video.avi', $file, function ($cli) {
    var_dump($cli->downloadFile);
}, $offset);
```

#### function swoole_http_client->close() : bool

Close the http connection.






