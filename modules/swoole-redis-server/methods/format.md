# Swoole Redis Server

## Methods

### swoole_redis_server::format

#### Prototype

```php
function swoole_redis_server::format(int $type, mixed $value = null);
```

#### Illustration

Format the data to the format of redis

#### Parameter

- `$format` the type of data. `NIL`, `ERROR`, `STATUS`, `INT`, `STRING`, `SET`, `MAP` 
