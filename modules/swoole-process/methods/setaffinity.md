# Swoole Process Manager

## Methods 

### swoole_process::setaffinity

#### Prototype

```php
bool swoole_process->setaffinity(array $cpu_set);
```

#### Illustration

Set the CPU affinity of the process.

#### Parameter

- `$cpu_set` the array of cpu number. Use `SWOOLE_CPU_NUM` to get the number of cpu. for example: array(0,2,3) stands for CPU0/CPU2/CPU3

#### Return

`true` : success, `false` : fail
