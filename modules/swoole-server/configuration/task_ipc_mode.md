## Configuration

### task_ipc_mode

Set the communication mode between the task worker process and worker process.

- `1`, default mode, use unix socket to communicate

- `2`, use the message queue to communicate

- `3`, use the message queue to communicate and set the mode to competition

> the difference between mode `2` and `3` : mode `2` supports the feature of sending task to a specified task worker process by `$serv->task($data, $task_worker_id)` while the mode `3` don't support to specify task worker process.

The message queue uses the memory queue provided by os to store the data. 

If [the configuration mssage_queue_key](/modules/swoole-server/configuration/message_queue_key.md) hasn't been seted, the message queue would use the private queue and this private queue would been deleted after the close of swoole server.

If [the configuration mssage_queue_key](/modules/swoole-server/configuration/message_queue_key.md) has been seted, the data of message queue would not be deleted and the swoole server could get the data after restart.

Use `ipcrm -q message_queue_id` to delete the data of message queue
