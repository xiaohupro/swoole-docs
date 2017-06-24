# Installation

#### Prerequisites

1. Operation system: Linux, FreeBSD or MacOS
2. Linux kernel version &gt;= 2.3.32
3. PHP version &gt;= 5.3.10
4. GCC version &gt;= 4.4 or Clang
5. Cmake version &gt;= 2.4 \(Cmake is not required to compile libswoole as C/C++ library\)

> Recommend Linux version: Ubuntu 14, CentOS 7 or greater.

#### Installation

##### Debian and Ubuntu users

``` bash
pecl install swoole
```

##### Fedora and RedHat users

``` bash
pecl install swoole
```

##### MacOS X \(macOS\) users

It is highly recommended to install Swoole on Mac OS X or macOS systems via homebrew:

``` bash
brew install swoole
```

##### Building swoole from sources

``` bash
phpize
./configure
make 
sudo make install
```

##### Configuration paramaters

``` bash
--enable-swoole-debug
```

Enable the debug logs of swoole, do not enable this in production environment.

``` bash
--enable-sockets
```

Enable sockets support, it depends on the PHP sockets extension. 

``` bash
--enable-openssl
``` 

Enable openssl support

``` bash
--with-openssl-dir
```

Change the default path of openssl library, for example:`--with-openssl-dir=/opt/openssl/.`

``` bash
--enable-http2
```

Enable the support of HTTP2, it depends on nghttp2 library.

``` bash
--enable-async-redis
```

Enable the suppor of async redis client, it depends on hiredis library.

``` bash
--enable-timewheel
```

Enable the support of timewheel, optimize the heartbeat algorithm.

``` bash
--enable-mysqlnd
```

Enable the support of mysqlnd, for example `swoole_mysql::escapse`

``` bash
--enable-ringbuffer
```

Enable the support of ringbuffer memory pool

> This is an experimental feature, do not use in production environment



