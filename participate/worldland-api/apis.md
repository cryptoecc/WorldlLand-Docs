---
description: web3.eth
---

# APIs

The `web3-eth` package allows you to interact with an Ethereum blockchain and Ethereum smart contracts.

```
var Eth = require('web3-eth');

// "Eth.providers.givenProvider" will be set if in an Ethereum supported browser.
var eth = new Eth('https://rpc.lvscan.io');

// or using the web3 umbrella package

var Web3 = require('web3');
var web3 = new Web3('https://rpc.lvscan.io');

// -> web3.eth
```



### Note on checksum addresses

All Ethereum addresses returned by functions of this package are returned as checksum addresses. This means some letters are uppercase and some are lowercase. Based on that it will calculate a checksum for the address and prove its correctness. Incorrect checksum addresses will throw an error when passed into functions. If you want to circumvent the checksum check you can make an address all lower- or uppercase.



#### Example

```
web3.eth.getAccounts(console.log);
> ['0xEf24Df7D15A977CA5318E3952e2F4dAcf636d37E', '0xb04fbC49bcd4c7dc1b4d77Fbceaf451fcfd3657A']
```



### Subscribe

For `web3.eth.subscribe` see the [Subscribe reference documentation](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-subscribe.html#eth-subscribe).

### Contract

For `web3.eth.Contract` see the [Contract reference documentation](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-contract.html#eth-contract).

### Iban

For `web3.eth.Iban` see the [Iban reference documentation](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-iban.html#eth-iban).

### personal

For `web3.eth.personal` see the [personal reference documentation](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-personal.html#eth-personal).

### accounts

For `web3.eth.accounts` see the [accounts reference documentation](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-accounts.html#eth-accounts).

### ens

For `web3.eth.ens` see the [ENS reference documentation](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-ens.html#eth-ens).

### abi

For `web3.eth.abi` see the [ABI reference documentation](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-abi.html#eth-abi).

### net

For `web3.eth.net` see the [net reference documentation](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-net.html#eth-net).

### setProvider

```
web3.setProvider('https://rpc.lvscan.io')
web3.eth.setProvider('https://rpc.lvscan.io')
web3.shh.setProvider('https://rpc.lvscan.io')
web3.bzz.setProvider('https://rpc.lvscan.io')
...
```



Will change the provider for its module.

❗️When called on the umbrella package `web3` it will also set the provider for all sub modules `web3.eth`, `web3.shh`, etc. EXCEPT `web3.bzz` which needs a separate provider at all times.



#### Example: Local Geth Node

```
var Web3 = require('web3');
var web3 = new Web3('https://rpc.lvscan.io');
// or
var web3 = new Web3(new Web3.providers.HttpProvider('https://rpc.lvscan.io'));

// change provider
web3.setProvider('https://rpc.lvscan.io');
// or
web3.setProvider(new Web3.providers.WebsocketProvider('https://rpc.lvscan.io'));

// Using the IPC provider in node.js
var net = require('net');
var web3 = new Web3('/Users/myuser/Library/Ethereum/geth.ipc', net); // mac os path
// or
var web3 = new Web3(new Web3.providers.IpcProvider('/Users/myuser/Library/Ethereum/geth.ipc', net)); // mac os path
// on windows the path is: "\\\\.\\pipe\\geth.ipc"
// on linux the path is: "/users/myuser/.ethereum/geth.ipc"
```



#### Example: Remote Node Provider

```
// Using a remote node provider, like Alchemy (https://www.alchemyapi.io/supernode), is simple.
var Web3 = require('web3');
var web3 = new Web3("https://eth-mainnet.alchemyapi.io/v2/your-api-key");
```



### providers

```
web3.providers
web3.eth.providers
web3.shh.providers
web3.bzz.providers
...
```

Contains the current available providers.\


#### Value

`Object` with the following providers:

> * `Object` - `HttpProvider`: HTTP provider, does not support subscriptions.
> * `Object` - `WebsocketProvider`: The Websocket provider is the standard for usage in legacy browsers.
> * `Object` - `IpcProvider`: The IPC provider is used node.js dapps when running a local node. Gives the most secure connection.



#### Example

```
var Web3 = require('web3');
// use the given Provider, e.g in Mist, or instantiate a new websocket provider
var web3 = new Web3(Web3.givenProvider || 'ws://remotenode.com:8546');
// or
var web3 = new Web3(Web3.givenProvider || new Web3.providers.WebsocketProvider('ws://remotenode.com:8546'));

// Using the IPC provider in node.js
var net = require('net');

var web3 = new Web3('/Users/myuser/Library/Ethereum/geth.ipc', net); // mac os path
// or
var web3 = new Web3(new Web3.providers.IpcProvider('/Users/myuser/Library/Ethereum/geth.ipc', net)); // mac os path
// on windows the path is: "\\\\.\\pipe\\geth.ipc"
// on linux the path is: "/users/myuser/.ethereum/geth.ipc"
```





































