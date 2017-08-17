## Method

### swoole_server->heartbeat

#### Prototype

```php
array swoole_server::heartbeat(bool $if_close_connection = true)
```

#### Illustration

Check status of all the connections of the server. Optionally close the idle and timeout connections.

#### Parameter

* `$if_close_connection`	the option which decides if close the connections which exceeds the time

#### Return

the array of connections

#### Example
