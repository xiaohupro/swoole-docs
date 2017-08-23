## Events and Callback functions 

### onManagerStop

The event `managerstop` happens when the manager process stops.

The callback function registered for event `managerstop` is called in the manager process.

#### Example

```
void onManagerStop(swoole_server $serv);
```
