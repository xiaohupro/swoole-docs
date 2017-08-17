## Method

### swoole_server->taskWaitMulti

#### Prototype

```php
array swoole_server->taskWaitMulti(array $tasks, double $timeout = 0.5)
```

#### Illustration

Execute multiple tasks concurrently

#### Parameter

* `$tasks`	the array of task data which is to send to the task worker, its type could any type except fot resource
* `$timeout`    the time of timeout 

#### Return

If the call of this method succeeds, the return is the array of the result of tasks
If the execution of some task exceeds the time of timeout, its result will not be in the return array

#### Example

``` php
<?php
$tasks[] = mt_rand(1000, 9999); 
$tasks[] = mt_rand(1000, 9999); 
$tasks[] = mt_rand(1000, 9999); 
var_dump($tasks);

$results = $serv->taskWaitMulti($tasks, 10.0);

if (!isset($results[0])) {
    echo "Task 1: timeout.\n";
}
if (isset($results[1])) {
    echo "Task 2: {$results[1]}\n";
}
if (isset($results[2])) {
    echo "Task 3: {$results[2]}\n";
}
```
