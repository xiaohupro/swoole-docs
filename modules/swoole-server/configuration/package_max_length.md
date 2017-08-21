## Configuration

### package_max_length

The max length of package whose unit is byte.

Once the configuration `open_length_check/open_eof_check/open_http_protocol` has enabled, the internal of swoole will joint the data received from the client amd the data stores in the memory before recevicing the whole package. So to limit the usage of memory, it should set the `package_max_length`.
