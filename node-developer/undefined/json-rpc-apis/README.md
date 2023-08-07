# JSON-RPC APIs

For interacting with the blockchain, ETH-ECC provides a **JSON-RPC API**. The JSON-RPC API interacts with ETH-ECC in the form of **JSON objects**. **RPC(Remote Procedure Call)** refers to sending a request to the ETH-ECC node as a JSON object from the outside. You can interact with ETH-ECC by sending a **JSON request** to the **RPC port** exposed by ETH-ECC. Since JSON-RPC is not user-friendly, APIs such as **web3** built on top of JSON-RPC provide user-friendly interfaces.



## JSON-RPC Server

ETH-ECC has three transport protocols that can use the JSON-RPC API. The following table summarizes the comparison of the three transport protocols. IPC is a private and secure protocol. **HTTP** is a friendly protocol and reduces message overhead for intermittent requests. For continuous request processing, a **WebSocket** server is a good choice.

<table data-header-hidden><thead><tr><th width="285"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td><strong>HTTP</strong></td><td><strong>WebSoket</strong></td><td><strong>IPC</strong></td></tr><tr><td>Subscribe to events</td><td>N</td><td><strong>Y</strong></td><td><strong>Y</strong></td></tr><tr><td>Remote Access</td><td><strong>Y</strong></td><td><strong>Y</strong></td><td>N</td></tr><tr><td>Metadata overhead per message</td><td>high</td><td>low</td><td>low</td></tr></tbody></table>



### HTTP Server <a href="#http-server" id="http-server"></a>

**HTTP** is a one-way transport protocol that connects clients and servers. The client sends a request to the server and the server returns a response to the client. The HTTP connection is closed after the response to the given request has been sent. HTTP is the most commonly used because it is a very common and familiar protocol. Including the **`-http` flag** in the command launches the HTTP server.

```sh
./worldland -http
```



The **HTTP** server runs on **localhost(127.0.0.1)** and **port 8545** by default. IP address and listening port This can be customized using the -http.addr and -http.port flags.

```sh
./worldland -http -http.port 3334 -http.addr 129.38.5.26
```



The HTTP server accepts only JSON-RPC requests for the **eth,net,web3 modules** by default. If you want to allow other modules, you must configure them using the **`-http.api`** flag.

{% hint style="warning" %}
Be careful with enabling additional API modules via HTTP as it increases your security risk.,
{% endhint %}

```sh
./worldland -http -http.api eth,net,web3
```



For **security** reasons, the HTTP server protects web pages from using APIs. To access the webpage, you need to add the webpage using the **`-http.corsdomain`** flag.

```sh
./worldland -http -http.corsdomain https://remix.ethereum.org
```

Add **'\*'** to allow all web pages.

```sh
./worldland -http.corsdomain '*'
```



### Websocket server

**Websocket** is a persistent, bidirectional transport protocol that keeps connections alive until terminated. Suitable for sending a large number of requests as it saves the **handshake procedure**. The flag command pattern is the same as for the HTTP server. The http command is replaced by ws. The default port for ws is 8546.

```sh
./worldland -ws -ws.port 3334 -ws.api eth,net,web3HTTP
```

Protecting webpage API requests is also the same, so use the `-ws.origins` flag for webpage requests.

```sh
./worldland -ws -ws.origins https://remix.ethereum.org
```



{% hint style="danger" %}
**HTTP and Websocket** servers allow external connections. This means that an **external attacker** can control the account inside ETH-ECC, so when the HTTP and Websocket servers are activated, the **node account** is **locked**. You can forcefully unlock an account by including the **`--allow-insecure-unlock` flag**, but this is not secure. Be aware that there are attacker bots constantly browsing the Ethereum HTTP server.
{% endhint %}



### IPC server

**IPC** can usually be used in a **local environment** where the node and console exist on the same machine. ETH-ECC creates a **local file socket** to connect to the node. The IPC server is enabled by default and has access to all JSON-RPC modules. Sockets are placed in the same directory as the node.

```sh
~/DATA_DIR/geth.ipc
```

In **Windows**, **IPC** is provided through named **pipes**. The default location of the pipe is:

```sh
\\.\pipe\geth.ipc
```

The location of the socket can be changed using the **`-ipcpath` flag** and disabled with the `-ipcdisable` flag.

```
./worldland -ipcpath -ipcdisable
```



## JSON-RPC Console



You can also start an **interactive session** by providing a **console** command when ETH-ECC starts. This will start the node and run the console in the same terminal. In this case, the **log** is output as well, so if not necessary, hide the log by redirecting it.

```
./worldland <other flags> console 2> /dev/null
```

You can redirect and save logs to a file. The level of detail provided in the logs can be tuned by supplying a value between 1-6 to the `-verbosity` flag, as shown in the example below.

```sh
./worldland <other flags> console --verbosity 3 2> worldland.log
```



You can interact with the node from the terminal console. The console supports the full JSON-RPC API.&#x20;

To check the balance of the first account that already exists in the keystore:

```javascript
eth.getBalance(eth.accounts[0]);
```

To send a transaction:

```javascript
eth.sendTransaction({
  to: eth.accounts[0],
  to: eth.accounts[1],
  value: web3.toWei(0.5, 'ether')
});
```

You can also load a **pre-built Javascript file** into the console by passing the --preload flag when starting the console.

```sh
geth console --preload "/my/scripts/folder/utils.js"
```

You can close the console by typing exit or **CTRL-D**.

```
exit
```

### &#x20;<a href="#non-interactive-use" id="non-interactive-use"></a>

## APIs

{% hint style="info" %}
ETH-ECC supports the same JSON-RPC module as Ethereum. See the JSON-RPC APIs of [ethereum](https://ethereum.org/en/developers/docs/apis/json-rpc/#json-rpc-methods) and [go-ethereum](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-admin) for details.
{% endhint %}

### &#x20;<a href="#non-interactive-use" id="non-interactive-use"></a>

