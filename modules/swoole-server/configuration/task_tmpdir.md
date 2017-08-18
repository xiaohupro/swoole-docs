## Configuration

### task_tmpdir

Set the path of temporary task data. 

If the data sended by task exceeds 8192 bytes, the swoole will use the temporary file to store the data.

The default of `task_tmpdir` is `/tmp`.
