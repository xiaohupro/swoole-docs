# Swoole Process Manager

## Methods

### Table of Contents

* [swoole_process->__construct(mixed $function, $redirect_stdin_stdout = false, $create_pipe = true)](/modules/swoole-process/methods/construct.md)
* [swoole_process->start()](/modules/swoole-process/methods/start.md)
* [swoole_process->name(string $new_process_name)](/modules/swoole-process/methods/name.md)
* [swoole_process->exec(string $execfile, array $args)](/modules/swoole-process/methods/exec.md)
* [swoole_process->write(string $data)](/modules/swoole-process/methods/write.md)
* [swoole_process->useQueue(int $msgkey = 0, int $mode = 2)](/modules/swoole-process/methods/usequeue.md)
* [swoole_process->statQueue()](/modules/swoole-process/methods/statqueue.md)
* [swoole_process->freeQueue()](/modules/swoole-process/methods/freequeue.md)
* [swoole_process->push()](/modules/swoole-process/methods/push.md)
* [swoole_process->pop(int $maxsize = 8192)](/modules/swoole-process/methods/pop.md)
* [swoole_process->close()](/modules/swoole-process/methods/close.md)
* [swoole_process->exit(int $status=0)](/modules/swoole-process/methods/exit.md)
* [swoole_process::kill($pid, $signo = SIGTERM)](/modules/swoole-process/methods/kill.md)
* [swoole_process::wait(bool $blocking = true)](/modules/swoole-process/methods/wait.md)
* [swoole_process::daemon(bool $nochdir = true, bool $noclose = true)](/modules/swoole-process/methods/daemon.md)
* [swoole_process::signal(int $signo, callable $callback)](/modules/swoole-process/methods/signal.md)
* [swoole_process::alarm(int $interval_usec, int $type = ITIMER_REAL)](/modules/swoole-process/methods/alarm.md)
* [swoole_process::setaffinity(array $cpu_set)](/modules/swoole-process/methods/setaffinity.md)
