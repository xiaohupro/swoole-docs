## Configuration 

### worker_num 

the number of the worker process

If the code of logic is asynchronous and non-blocking, set the `worker_num` to the value from one times to four times of cpu cores.
If the code of logic is synchronous and blocking, set the `worker_num` according to the consuming time of request and load of os.
