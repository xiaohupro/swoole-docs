## Configuration

### package_length_type

The type of length. For now, the swoole supports 10 types.

- c : signed, 1 byte
- C : unsigned, 1 byte
- s : signed, host byte order, 2 bytes
- S : unsigned, host byte order, 2 bytes
- n : unsigned, network byte order, 2 bytes
- N : unsigned, network byte order, 4 bytes
- l : signed, host byte order, 4 bytes
- L : unsigned, host byte order, 4 bytes
- v : unsigned, little endian, 2 bytes
- V : unsigned, little endian, 4 bytes
