## Configuration

### log_file

Set the log path of swoole.

#### Tips

In the log file, there are some labels to distinguish the thread or process that output the log item.

- `#` Master process

- `$` Manager process

- `*` Worker process

- `^` Task worker process

#### Reopen the log file

If the log file has been `mv` or `unlink`, the log can't be recorded normally. In this situation, you can send `SIGRTMIN` 
