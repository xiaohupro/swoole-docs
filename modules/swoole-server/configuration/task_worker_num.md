## Configuration

### task_worker_num

the number of task worker process.

To enable this parameter, it needs to register the callback function of `task` event and `finish` event.

The task worker process is synchronous and blocking.

According to the speed of sending task and handling task, set a reasonable value of `task_worker_num`.
