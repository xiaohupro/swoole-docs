# Swoole WebSocket server

## Predefined Contants

### Types of websocket data frame

- WEBSOCKET_OPCODE_TEXT = 0x1, utf8 text data

- WEBSOCKET_OPCODE_BINARY = 0x2, binary data

- WEBSOCKET_OPCODE_PING = 0x9, ping data

### Status of websocket connection

- WEBSOCKET_STATUS_CONNECTION = 1, connection created and wait for handshake

- WEBSOCKET_STATUS_HANDSHAKE = 2, in the process of handshake

- WEBSOCKET_STATUS_FRAME = 3, handshake finished and wait for tranforming message
