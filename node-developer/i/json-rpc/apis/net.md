# Net

The net API provides insight about the networking aspect of the client.

### net\_listening <a href="#net-listening" id="net-listening"></a>

Returns an indication if the node is listening for network connections.

| CLIENT  | METHOD INVOCATION            |
| ------- | ---------------------------- |
| Console | net.listening                |
| RPC     | {"method": "net\_listening"} |

### net\_peerCount <a href="#net-peercount" id="net-peercount"></a>

Returns the number of connected peers.

| CLIENT  | METHOD INVOCATION            |
| ------- | ---------------------------- |
| Console | net.peerCount                |
| RPC     | {"method": "net\_peerCount"} |

### net\_version <a href="#net-version" id="net-version"></a>

Returns the devp2p network ID (e.g. 1 for mainnet, 5 for goerli).

| CLIENT  | METHOD INVOCATION          |
| ------- | -------------------------- |
| Console | net.version                |
| RPC     | {"method": "net\_version"} |
