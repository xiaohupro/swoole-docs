## Configuration

### task_max_request

the max number of task the task worker process could handle. 

After handling the number of `task_max_request` tasks, the task worker process will exit and release all the memory amd resouce occupied by this process. And then, the manager will respawn a new task worker process.

The dafault value of `task_max_request` is 0 which means there is no limit of the max task request.
