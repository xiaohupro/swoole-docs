## Configuration

### discard_timeout_request

If the configuration of `dispatch_mode` is 1 or 3, there may be some data that arrive to worker process after closing the connection.

In this situation, if `discard_timeout_request` is true, the worker process will discard these data or still procee these data.
