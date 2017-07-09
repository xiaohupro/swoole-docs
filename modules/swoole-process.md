# Swoole Process Manager

Swoole process manager can be used to replace PHP *pcntl* extension. Compare with PHP pcntl, Swoole process manager provides more features:

* Interprocess communication based on unixsock, with read/write or push/pop API.
* Redirect standard input and output
* The child process can use swoole_event callbacks.
* Exec API enable the child process execute Linux applications and communicate with parent process

### Example

``` php
<?php
(new class{
    public $mpid=0;
    public $works=[];
    public $max_precess=1;
    public $new_index=0;

    public function __construct(){
        try {
            swoole_set_process_name(sprintf('php-ps:%s', 'master'));
            $this->mpid = posix_getpid();
            $this->run();
            $this->processWait();
        }catch (\Exception $e){
            die('ALL ERROR: '.$e->getMessage());
        }
    }

    public function run(){
        for ($i=0; $i < $this->max_precess; $i++) {
            $this->CreateProcess();
        }
    }

    public function CreateProcess($index=null){
        $process = new swoole_process(function(swoole_process $worker)use($index){
            if(is_null($index)){
                $index=$this->new_index;
                $this->new_index++;
            }
            swoole_set_process_name(sprintf('php-ps:%s',$index));
            for ($j = 0; $j < 16000; $j++) {
                $this->checkMpid($worker);
                echo "msg: {$j}\n";
                sleep(1);
            }
        }, false, false);
        $pid=$process->start();
        $this->works[$index]=$pid;
        return $pid;
    }
    public function checkMpid(&$worker){
        if(!swoole_process::kill($this->mpid,0)){
            $worker->exit();
            echo "Master process exited, I [{$worker['pid']}] also quit\n";
        }
    }

    public function rebootProcess($ret){
        $pid=$ret['pid'];
        $index=array_search($pid, $this->works);
        if($index!==false){
            $index=intval($index);
            $new_pid=$this->CreateProcess($index);
            echo "rebootProcess: {$index}={$new_pid} Done\n";
            return;
        }
        throw new \Exception('rebootProcess Error: no pid');
    }

    public function processWait(){
        while(1) {
            if(count($this->works)){
                $ret = swoole_process::wait();
                if ($ret) {
                    $this->rebootProcess($ret);
                }
            }else{
                break;
            }
        }
    }
});
```

### Methods

#### int swoole_process->__construct(mixed $function, $redirect_stdin_stdout = false, $create_pipe = true);

Construct a child process with the callback function executed in the child process, optionally redirect the standard I/O to pipes between the parent process and the child processes.

> When the parent process is stopped, the child processes will receive *CLOSE* event from the pipe.

#### int swoole_process->start();

Fork the swoole child process constructed and return the *PID* of the child process, or return false if the fork is failed. 

Attributes of the child process:

``` php
<?php
$process->pid
$process->pipe
```

#### bool swoole_process->name(string $new_process_name);

Set name of the process started.

#### bool swoole_process->exec(string $execfile, array $args)

Execute system commands:

* $execfile is the path of the command.
* $args are the arguments for the command.

The process will be replaced to be the system command process, but the pipe between the parent process will be kept.

#### int swoole_process->write(string $data);

Write data into the pipe and communicate with the parent process or child processes.

#### int swoole_process->read(int $buffer_size=8192);

Read data from the pipe:

#### bool swoole_process->useQueue(int $msgkey = 0, int $mode = 2);

Create a message queue as the communication method between the parent process and child processes.

* $msgkey is the ID of the message queue, the default value is *ftok(__FILE__, 1)*

#### array swoole_process->statQueue();

Get the stats of the message queue used as the communication method between processes.

#### function swoole_process->freeQueue();

Destory the message queue created by *swoole_process->useQueue(int $msgkey = 0, int $mode = 2)*.

#### bool swoole_process->push(string $data);

Write and push data into the message queue.

Example:

``` php
<?php

$workers = [];
$worker_num = 2;

for($i = 0; $i < $worker_num; $i++)
{
    $process = new swoole_process('callback_function', false, false);
    $process->useQueue();
    $pid = $process->start();
    $workers[$pid] = $process;
}

function callback_function(swoole_process $worker)
{
    echo "Child process started, PID=".$worker->pid."\n";
    //recv data from the parent process
    $recv = $worker->pop();
    echo "Data received from the parent process: $recv\n";
    sleep(2);
    $worker->exit(0);
}

foreach($workers as $pid => $process)
{
    $process->push("hello child process [$pid]\n");
}

for($i = 0; $i < $worker_num; $i++)
{
    $ret = swoole_process::wait();
    $pid = $ret['pid'];
    unset($workers[$pid]);
    echo "Child process exit, PID=".$pid.PHP_EOL;
}
```

#### string swoole_process->pop(int $maxsize = 8192);

Read and pop data from the message queue.

#### bool swoole_process->close();

Close the pipe of the child process.

#### int swoole_process->exit(int $status=0);

Stop the child process.

#### int swoole_process->kill($pid, $signo = SIGTERM);

Send signal to the child process.

#### array swoole_process->wait(bool $blocking = true);

Wait for the events of child processes.

#### bool swoole_process->daemon(bool $nochdir = true, bool $noclose = true);

Change the process to be a daemon process.

* $nochdir: whether change the current path.
* $noclose: whether close the standard I/O of the process.

#### bool swoole_process->signal(int $signo, callable $callback);

Setup signal callback function.

#### swoole_process->alarm(int $interval_usec, int $type = ITIMER_REAL) : bool

#### swoole_process->setaffinity(array $cpu_set);

Set the CPU affinity of the process.



