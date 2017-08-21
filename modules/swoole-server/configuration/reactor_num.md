## Configuration 

### reactor_num 

the number of the reactor thread(for SWOOLE_BASE_MODE)

You can change the number of event processing thread in the master process. 

To make full use of cpu, the default number of `reactor_num` is the number of core in cpu.

In general, the number of the reactor thread is between one and four times of cpu cores.
