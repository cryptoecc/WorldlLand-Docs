---
description: web3.eth
---

# Web3 api

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



#### Configuration

```
// ====
// Http
// ====

var Web3HttpProvider = require('web3-providers-http');

var options = {
    keepAlive: true,
    withCredentials: false,
    timeout: 20000, // ms
    headers: [
        {
            name: 'Access-Control-Allow-Origin',
            value: '*'
        },
        {
            ...
        }
    ],
    agent: {
        http: http.Agent(...),
        baseUrl: ''
    }
};

var provider = new Web3HttpProvider('http://localhost:8545', options);

// ==========
// Websockets
// ==========

var Web3WsProvider = require('web3-providers-ws');

var options = {
    timeout: 30000, // ms

    // Useful for credentialed urls, e.g: ws://username:password@localhost:8546
    headers: {
      authorization: 'Basic username:password'
    },

    clientConfig: {
      // Useful if requests are large
      maxReceivedFrameSize: 100000000,   // bytes - default: 1MiB
      maxReceivedMessageSize: 100000000, // bytes - default: 8MiB

      // Useful to keep a connection alive
      keepalive: true,
      keepaliveInterval: 60000 // ms
    },

    // Enable auto reconnection
    reconnect: {
        auto: true,
        delay: 5000, // ms
        maxAttempts: 5,
        onTimeout: false
    }
};

var ws = new Web3WsProvider('ws://localhost:8546', options);
```



More information for the Http and Websocket provider modules can be found here:

> * [HttpProvider](https://github.com/ethereum/web3.js/tree/1.x/packages/web3-providers-http#usage)
> * [WebsocketProvider](https://github.com/ethereum/web3.js/tree/1.x/packages/web3-providers-ws#usage)



### givenProvider

```
web3.givenProvider
web3.eth.givenProvider
web3.shh.givenProvider
web3.bzz.givenProvider
...
```



When using web3.js in an Ethereum compatible browser, it will set with the current native provider by that browser. Will return the given provider by the (browser) environment, otherwise `null`.



#### Returns

`Object`: The given provider set or `null`;



#### Example



### currentProvider

```
web3.currentProvider
web3.eth.currentProvider
web3.shh.currentProvider
web3.bzz.currentProvider
...
```

Will return the current provider, otherwise `null`.

#### Returns

`Object`: The current provider set or `null`.

#### Example

***

### BatchRequest

```
new web3.BatchRequest()
new web3.eth.BatchRequest()
new web3.shh.BatchRequest()
new web3.bzz.BatchRequest()
```

Class to create and execute batch requests.

#### Parameters

none

#### Returns

`Object`: With the following methods:

> * `add(request)`: To add a request object to the batch call.
> * `execute()`: Will execute the batch request.

#### Example

```
var contract = new web3.eth.Contract(abi, address);

var batch = new web3.BatchRequest();
batch.add(web3.eth.getBalance.request('0x0000000000000000000000000000000000000000', 'latest', callback));
batch.add(contract.methods.balance(address).call.request({from: '0x0000000000000000000000000000000000000000'}, callback2));
batch.execute();
```

***

### extend

```
web3.extend(methods)
web3.eth.extend(methods)
web3.shh.extend(methods)
web3.bzz.extend(methods)
...
```

Allows extending the web3 modules.

Note

You also have `*.extend.formatters` as additional formatter functions to be used for input and output formatting. Please see the [source file](https://github.com/ethereum/web3.js/blob/1.x/packages/web3-core-helpers/src/formatters.js) for function details.

#### Parameters

1. `methods` - `Object`: Extension object with array of methods description objects as follows:
   * `property` - `String`: (optional) The name of the property to add to the module. If no property is set it will be added to the module directly.
   * `methods` - `Array`: The array of method descriptions:
     * `name` - `String`: Name of the method to add.
     * `call` - `String`: The RPC method name.
     * `params` - `Number`: (optional) The number of parameters for that function. Default 0.
     * `inputFormatter` - `Array`: (optional) Array of inputformatter functions. Each array item responds to a function parameter, so if you want some parameters not to be formatted, add a `null` instead.
     * `outputFormatter - ``Function`: (optional) Can be used to format the output of the method.

#### Returns

`Object`: The extended module.

#### Example

```
web3.extend({
    property: 'myModule',
    methods: [{
        name: 'getBalance',
        call: 'eth_getBalance',
        params: 2,
        inputFormatter: [web3.extend.formatters.inputAddressFormatter, web3.extend.formatters.inputDefaultBlockNumberFormatter],
        outputFormatter: web3.utils.hexToNumberString
    },{
        name: 'getGasPriceSuperFunction',
        call: 'eth_gasPriceSuper',
        params: 2,
        inputFormatter: [null, web3.utils.numberToHex]
    }]
});

web3.extend({
    methods: [{
        name: 'directCall',
        call: 'eth_callForFun',
    }]
});

console.log(web3);
> Web3 {
    myModule: {
        getBalance: function(){},
        getGasPriceSuperFunction: function(){}
    },
    directCall: function(){},
    eth: Eth {...},
    bzz: Bzz {...},
    ...
}
```

***

***

### defaultAccount

```
web3.eth.defaultAccount
```

This default address is used as the default `"from"` property, if no `"from"` property is specified in for the following methods:

* [web3.eth.sendTransaction()](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-sendtransaction)
* web3.eth.call()
* new web3.eth.Contract() -> myContract.methods.myMethod().call()
* new web3.eth.Contract() -> myContract.methods.myMethod().send()

#### Property

`String` - 20 Bytes: Any ethereum address. You should have the private key for that address in your node or keystore. (Default is `undefined`)

#### Example

```
web3.eth.defaultAccount;
> undefined

// set the default account
web3.eth.defaultAccount = '0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe';
```

***

### defaultBlock

```
web3.eth.defaultBlock
```

The default block is used for certain methods. You can override it by passing in the defaultBlock as last parameter. The default value is `"latest"`.

* web3.eth.getBalance()
* web3.eth.getCode()
* [web3.eth.getTransactionCount()](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-gettransactioncount)
* web3.eth.getStorageAt()
* web3.eth.call()
* new web3.eth.Contract() -> myContract.methods.myMethod().call()

#### Property

Default block parameters can be one of the following:

* `Number|BN|BigNumber`: A block number
* `"earliest"` - `String`: The genesis block
* `"latest"` - `String`: The latest block (current head of the blockchain)
* `"pending"` - `String`: The currently mined block (including pending transactions)
* `"finalized"` - `String`: (For POS networks) The finalized block is one which has been accepted as canonical by >2/3 of validators.
* `"safe"` - `String`: (For POS networks) The safe head block is one which under normal network conditions, is expected to be included in the canonical chain. Under normal network conditions the safe head and the actual tip of the chain will be equivalent (with safe head trailing only by a few seconds). Safe heads will be less likely to be reorged than the proof of work networks latest blocks.

Default is `"latest"`

#### Example

```
web3.eth.defaultBlock;
> "latest"

// set the default block
web3.eth.defaultBlock = 231;
```

### defaultHardfork

```
web3.eth.defaultHardfork
```

The default hardfork property is used for signing transactions locally.

#### Property

The default hardfork property can be one of the following:

* `"chainstart"` - `String`
* `"homestead"` - `String`
* `"dao"` - `String`
* `"tangerineWhistle"` - `String`
* `"spuriousDragon"` - `String`
* `"byzantium"` - `String`
* `"constantinople"` - `String`
* `"petersburg"` - `String`
* `"istanbul"` - `String`
* `"berlin"` - `String`
* `"london"` - `String`

Default is `"london"`

#### Example

```
web3.eth.defaultHardfork;
> "london"

// set the default block
web3.eth.defaultHardfork = 'istanbul';
```

### defaultChain

```
web3.eth.defaultChain
```

The default chain property is used for signing transactions locally.

#### Property

The default chain property can be one of the following:

* `"mainnet"` - `String`
* `"goerli"` - `String`
* `"kovan"` - `String`
* `"rinkeby"` - `String`
* `"ropsten"` - `String`

Default is `"mainnet"`

#### Example

```
web3.eth.defaultChain;
> "mainnet"

// set the default chain
web3.eth.defaultChain = 'goerli';
```

### defaultCommon

```
web3.eth.defaultCommon
```

The default common property is used for signing transactions locally.

#### Property

The default common property does contain the following `Common` object:

* `customChain` - `Object`: The custom chain properties
  * `name` - `string`: (optional) The name of the chain
  * `networkId` - `number`: Network ID of the custom chain
  * `chainId` - `number`: Chain ID of the custom chain
* `baseChain` - `string`: (optional) `mainnet`, `goerli`, `kovan`, `rinkeby`, or `ropsten`
* `hardfork` - `string`: (optional) `chainstart`, `homestead`, `dao`, `tangerineWhistle`, `spuriousDragon`, `byzantium`, `constantinople`, `petersburg`, `istanbul`, `berlin`, or `london`

Default is `undefined`.

#### Example

```
web3.eth.defaultCommon;
> {customChain: {name: 'custom-network', chainId: 1, networkId: 1}, baseChain: 'mainnet', hardfork: 'petersburg'}

// set the default common
web3.eth.defaultCommon = {customChain: {name: 'custom-network', chainId: 1, networkId: 1}, baseChain: 'mainnet', hardfork: 'petersburg'};
```

***

### transactionBlockTimeout

```
web3.eth.transactionBlockTimeout
```

The `transactionBlockTimeout` is used over socket-based connections. This option defines the amount of new blocks it should wait until the first confirmation happens, otherwise the PromiEvent rejects with a timeout error.

#### Returns

`number`: The current value of transactionBlockTimeout (default: 50)

#### Example

```
web3.eth.transactionBlockTimeout;
> 50

// set the transaction block timeout
web3.eth.transactionBlockTimeout = 100;
```

***

### blockHeaderTimeout

```
web3.eth.Contract.blockHeaderTimeout
contract.blockHeaderTimeout // on contract instance
```

The `blockHeaderTimeout` is used over socket-based connections. This option defines the amount seconds it should wait for “newBlockHeaders” event before falling back to polling to fetch transaction receipt.

#### Returns

`number`: The current value of blockHeaderTimeout (default: 10 seconds)

#### Example

```
web3.eth.blockHeaderTimeout;
> 5

// set the transaction confirmations blocks
web3.eth.blockHeaderTimeout = 10;
```

***

### transactionConfirmationBlocks

```
web3.eth.transactionConfirmationBlocks
```

This defines the number of blocks it requires until a transaction is considered confirmed.

#### Returns

`number`: The current value of transactionConfirmationBlocks (default: 24)

#### Example

```
web3.eth.transactionConfirmationBlocks;
> 24

// set the transaction confirmations blocks
web3.eth.transactionConfirmationBlocks = 50;
```

***

### transactionPollingTimeout

```
web3.eth.transactionPollingTimeout
```

The `transactionPollingTimeout` is used over HTTP connections. This option defines the number of seconds Web3 will wait for a receipt which confirms that a transaction was mined by the network. Note: If this method times out, the transaction may still be pending.

#### Returns

`number`: The current value of transactionPollingTimeout (default: 750)

#### Example

```
web3.eth.transactionPollingTimeout;
> 750

// set the transaction polling timeout
web3.eth.transactionPollingTimeout = 1000;
```

***

### transactionPollingInterval

```
web3.eth.transactionPollingInterval
```

The `transactionPollingInterval` is used over HTTP connections. This option defines the number of seconds between Web3 calls for a receipt which confirms that a transaction was mined by the network.

#### Returns

`number`: The current value of transactionPollingInterval (default: 1000ms)

***

### handleRevert

```
web3.eth.handleRevert
```

The `handleRevert` options property defaults to `false` and returns the revert reason string if enabled for the following methods:

* web3.eth.call()
* [web3.eth.sendTransaction()](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-sendtransaction)
* [contract.methods.myMethod(…).send(…)](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-contract.html#contract-send)
* [contract.methods.myMethod(…).call(…)](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-contract.html#contract-call)

Note

The revert reason string and signature exist as a property on the returned error.

#### Returns

`boolean`: The current value of `handleRevert` (default: false)

#### Example

```
web3.eth.handlRevert;
> false

// turn revert handling on
web3.eth.handleRevert = true;
```

***

### maxListenersWarningThreshold

```
web3.eth.maxListenersWarningThreshold
```

This defines the threshold above which a warning about the number of event listeners attached to a provider which supports sockets subscriptions will be written to the console. You may see this warning if you call `setProvider` on large numbers of Web3 contract objects.

#### Returns

`number`: The current value of maxListenersWarningThreshold (default: 100)

#### Example

```
web3.eth.maxListenersWarningThreshold;
> 100

// set the max listeners warning threshold
web3.eth.maxListenersWarningThreshold = 200;
```

***

### getProtocolVersion

```
web3.eth.getProtocolVersion([callback])
```

Returns the ethereum protocol version of the node.

#### Returns

`Promise` returns `String`: the protocol version.

#### Example

```
web3.eth.getProtocolVersion()
.then(console.log);
> "63"
```

***

### isSyncing

```
web3.eth.isSyncing([callback])
```

Checks if the node is currently syncing and returns either a syncing object, or `false`.

#### Returns

`Promise` returns `Object|Boolean` - A sync object when the node is currently syncing or `false`:

> * `startingBlock` - `Number`: The block number where the sync started.
> * `currentBlock` - `Number`: The block number where the node is currently synced to.
> * `highestBlock` - `Number`: The estimated block number to sync to.
> * `knownStates` - `Number`: The number of estimated states to download.
> * `pulledStates` - `Number`: The number of already downloaded states.

#### Example

```
web3.eth.isSyncing()
.then(console.log);

> {
    startingBlock: 100,
    currentBlock: 312,
    highestBlock: 512,
    knownStates: 234566,
    pulledStates: 123455
}
```

***

### getCoinbase

```
getCoinbase([callback])
```

Returns the coinbase address to which mining rewards will go.

#### Returns

`Promise` returns `String` - bytes 20: The coinbase address set in the node for mining rewards.

#### Example

```
web3.eth.getCoinbase()
.then(console.log);
> "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe"
```

***

### isMining

```
web3.eth.isMining([callback])
```

Checks whether the node is mining or not.

#### Returns

`Promise` returns `Boolean`: `true` if the node is mining, otherwise `false`.

#### Example

```
web3.eth.isMining()
.then(console.log);
> true
```

***

### getHashrate

```
web3.eth.getHashrate([callback])
```

Returns the number of hashes per second that the node is mining with.

#### Returns

`Promise` returns `Number`: Number of hashes per second.

#### Example

```
web3.eth.getHashrate()
.then(console.log);
> 493736
```

***

### getGasPrice

```
web3.eth.getGasPrice([callback])
```

Returns the current gas price oracle. The gas price is determined by the last few blocks median gas price.

#### Returns

`Promise` returns `String` - Number string of the current gas price in wei.

See the [A note on dealing with big numbers in JavaScript](https://web3js.readthedocs.io/en/v1.8.2/web3-utils.html#utils-bn).

#### Example

```
web3.eth.getGasPrice()
.then(console.log);
> "20000000000"
```

***

### getFeeHistory

```
web3.eth.getFeeHistory(blockCount, newestBlock, rewardPercentiles, [callback])
```

Transaction fee history Returns base fee per gas and transaction effective priority fee per gas history for the requested block range if available. The range between headBlock-4 and headBlock is guaranteed to be available while retrieving data from the pending block and older history are optional to support. For pre-EIP-1559 blocks the gas prices are returned as rewards and zeroes are returned for the base fee per gas.

#### Parameters

1. `String|Number|BN|BigNumber` - Number of blocks in the requested range. Between 1 and 1024 blocks can be requested in a single query. Less than requested may be returned if not all blocks are available.
2. `String|Number|BN|BigNumber` - Highest number block of the requested range.
3. `Array of numbers` - A monotonically increasing list of percentile values to sample from each block’s effective priority fees per gas in ascending order, weighted by gas used. Example: _\[“0”, “25”, “50”, “75”, “100”]_ or _\[“0”, “0.5”, “1”, “1.5”, “3”, “80”]_
4. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Object` - Fee history for the returned block range. The object:

* `Number` oldestBlock - Lowest number block of the returned range.
* `Array of strings` baseFeePerGas - An array of block base fees per gas. This includes the next block after the newest of the returned range, because this value can be derived from the newest block. Zeroes are returned for pre-EIP-1559 blocks.
* `Array of numbers` gasUsedRatio - An array of block gas used ratios. These are calculated as the ratio of gasUsed and gasLimit.
* `Array of string arrays` reward - An array of effective priority fee per gas data points from a single block. All zeroes are returned if the block is empty.

***

### getAccounts

```
web3.eth.getAccounts([callback])
```

Returns a list of accounts the node controls.

#### Returns

`Promise` returns `Array` - An array of addresses controlled by node.

#### Example

```
web3.eth.getAccounts()
.then(console.log);
> ["0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe", "0xDCc6960376d6C6dEa93647383FfB245CfCed97Cf"]
```

***

### getBlockNumber

```
web3.eth.getBlockNumber([callback])
```

Returns the current block number.

#### Returns

`Promise` returns `Number` - The number of the most recent block.

#### Example

```
web3.eth.getBlockNumber()
.then(console.log);
> 2744
```

***

### getBalance

```
web3.eth.getBalance(address [, defaultBlock] [, callback])
```

Get the balance of an address at a given block.

#### Parameters

1. `String` - The address to get the balance of.
2. `Number|String|BN|BigNumber` - (optional) If you pass this parameter it will not use the default block set with [web3.eth.defaultBlock](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock). Pre-defined block numbers as `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` can also be used.
3. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `String` - The current balance for the given address in wei.

See the [A note on dealing with big numbers in JavaScript](https://web3js.readthedocs.io/en/v1.8.2/web3-utils.html#utils-bn).

#### Example

```
web3.eth.getBalance("0x407d73d8a49eeb85d32cf465507dd71d507100c1")
.then(console.log);
> "1000000000000"
```

***

### getStorageAt

```
web3.eth.getStorageAt(address, position [, defaultBlock] [, callback])
```

Get the storage at a specific position of an address.

#### Parameters

1. `String` - The address to get the storage from.
2. `Number|String|BN|BigNumber` - The index position of the storage.
3. `Number|String|BN|BigNumber` - (optional) If you pass this parameter it will not use the default block set with [web3.eth.defaultBlock](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock). Pre-defined block numbers as `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` can also be used.
4. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `String` - The value in storage at the given position.

#### Example

```
web3.eth.getStorageAt("0x407d73d8a49eeb85d32cf465507dd71d507100c1", 0)
.then(console.log);
> "0x033456732123ffff2342342dd12342434324234234fd234fd23fd4f23d4234"
```

***

### getCode

```
web3.eth.getCode(address [, defaultBlock] [, callback])
```

Get the code at a specific address.

#### Parameters

1. `String` - The address to get the code from.
2. `Number|String|BN|BigNumber` - (optional) If you pass this parameter it will not use the default block set with [web3.eth.defaultBlock](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock). Pre-defined block numbers as `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` can also be used.
3. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `String` - The data at given address `address`.

#### Example

```
web3.eth.getCode("0xd5677cf67b5aa051bb40496e68ad359eb97cfbf8")
.then(console.log);
> "0x600160008035811a818181146012578301005b601b6001356025565b8060005260206000f25b600060078202905091905056"
```

***

### getBlock

```
web3.eth.getBlock(blockHashOrBlockNumber [, returnTransactionObjects] [, callback])
```

Returns a block matching the block number or block hash.

#### Parameters

1. `String|Number|BN|BigNumber` - The block number or block hash. Or the string `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` as in the [default block parameter](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock).
2. `Boolean` - (optional, default `false`) If specified `true`, the returned block will contain all transactions as objects. If `false` it will only contains the transaction hashes.
3. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Object` - The block object:

> * `number` - `Number`: The block number. `null` if a pending block.
> * `hash` 32 Bytes - `String`: Hash of the block. `null` if a pending block.
> * `parentHash` 32 Bytes - `String`: Hash of the parent block.
> * `baseFeePerGas` - `Number`: Minimum to be charged to send a transaction on the network
> * `codeword` - `String`: Hash of the generated proof-of-work. `null` if a pending block.
> * `nonce` 8 Bytes - `String`: Hash of the generated proof-of-work. `null` if a pending block.
> * `sha3Uncles` 32 Bytes - `String`: SHA3 of the uncles data in the block.
> * `logsBloom` 256 Bytes - `String`: The bloom filter for the logs of the block. `null` if a pending block.
> * `transactionsRoot` 32 Bytes - `String`: The root of the transaction trie of the block.
> * `stateRoot` 32 Bytes - `String`: The root of the final state trie of the block.
> * `miner` - `String`: The address of the beneficiary to whom the mining rewards were given.
> * `difficulty` - `String`: Integer of the difficulty for this block.
> * `totalDifficulty` - `String`: Integer of the total difficulty of the chain until this block.
> * `extraData` - `String`: The “extra data” field of this block.
> * `size` - `Number`: Integer the size of this block in bytes.
> * `gasLimit` - `Number`: The maximum gas allowed in this block.
> * `gasUsed` - `Number`: The total used gas by all transactions in this block.
> * `timestamp` - `Number`: The unix timestamp for when the block was collated.
> * `transactions` - `Array`: Array of transaction objects, or 32 Bytes transaction hashes depending on the `returnTransactionObjects` parameter.
> * `uncles` - `Array`: Array of uncle hashes.

#### Example

```
web3.eth.getBlock(3150)
.then(console.log);

> {
    "number": 3,
    "hash": "0xef95f2f1ed3ca60b048b4bf67cde2195961e0bba6f70bcbea9a2c4e133e34b46",
    "parentHash": "0x2302e1c0b972d00932deb5dab9eb2982f570597d9d42504c05d9c2147eaf9c88",
    "baseFeePerGas": 58713056622,
    "nonce": "0xfb6e1a62d119228b",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "transactionsRoot": "0x3a1b03875115b79539e5bd33fb00d8f7b7cd61929d5a3c574f507b8acf415bee",
    "stateRoot": "0xf1133199d44695dfa8fd1bcfe424d82854b5cebef75bddd7e40ea94cda515bcb",
    "miner": "0x8888f1f195afa192cfee860698584c030f4c9db1",
    "difficulty": '21345678965432',
    "totalDifficulty": '324567845321',
    "size": 616,
    "extraData": "0x",
    "gasLimit": 3141592,
    "gasUsed": 21662,
    "timestamp": 1429287689,
    "transactions": [
        "0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b"
    ],
    "uncles": []
}
```

***

### getBlockTransactionCount

```
web3.eth.getBlockTransactionCount(blockHashOrBlockNumber [, callback])
```

Returns the number of transaction in a given block.

#### Parameters

1. `String|Number|BN|BigNumber` - The block number or hash. Or the string `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` as in the [default block parameter](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock).
2. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Number` - The number of transactions in the given block.

#### Example

```
web3.eth.getBlockTransactionCount("0x407d73d8a49eeb85d32cf465507dd71d507100c1")
.then(console.log);
> 1
```

***

### getBlockUncleCount

```
web3.eth.getBlockUncleCount(blockHashOrBlockNumber [, callback])
```

Returns the number of uncles in a block from a block matching the given block hash.

#### Parameters

1. `String|Number|BN|BigNumber` - The block number or hash. Or the string `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` as in the [default block parameter](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock).
2. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Number` - The number of transactions in the given block.

#### Example

```
web3.eth.getBlockUncleCount("0x407d73d8a49eeb85d32cf465507dd71d507100c1")
.then(console.log);
> 1
```

***

### getUncle

```
web3.eth.getUncle(blockHashOrBlockNumber, uncleIndex [, returnTransactionObjects] [, callback])
```

Returns a blocks uncle by a given uncle index position.

#### Parameters

1. `String|Number|BN|BigNumber` - The block number or hash. Or the string `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` as in the [default block parameter](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock).
2. `Number` - The index position of the uncle.
3. `Boolean` - (optional, default `false`) If specified `true`, the returned block will contain all transactions as objects. By default it is `false` so, there is no need to explictly specify false. And, if `false` it will only contains the transaction hashes.
4. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Object` - the returned uncle. For a return value see [web3.eth.getBlock()](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-getblock).

Note

An uncle doesn’t contain individual transactions.

#### Example

```
web3.eth.getUncle(500, 0)
.then(console.log);
> // see web3.eth.getBlock
```

***

### getTransaction

```
web3.eth.getTransaction(transactionHash [, callback])
```

Returns a transaction matching the given transaction hash.

#### Parameters

1. `String` - The transaction hash.
2. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Object` - A transaction object its hash `transactionHash`:

> * `hash` 32 Bytes - `String`: Hash of the transaction.
> * `nonce` - `Number`: The number of transactions made by the sender prior to this one.
> * `blockHash` 32 Bytes - `String`: Hash of the block where this transaction was in. `null` if pending.
> * `blockNumber` - `Number`: Block number where this transaction was in. `null` if pending.
> * `transactionIndex` - `Number`: Integer of the transactions index position in the block. `null` if pending.
> * `from` - `String`: Address of the sender.
> * `to` - `String`: Address of the receiver. `null` if it’s a contract creation transaction.
> * `value` - `String`: Value transferred in wei.
> * `gasPrice` - `String`: Gas price provided by the sender in wei.
> * `gas` - `Number`: Gas provided by the sender.
> * `input` - `String`: The data sent along with the transaction.

#### Example

```
web3.eth.getTransaction('0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b§234')
.then(console.log);

> {
    "hash": "0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b",
    "nonce": 2,
    "blockHash": "0xef95f2f1ed3ca60b048b4bf67cde2195961e0bba6f70bcbea9a2c4e133e34b46",
    "blockNumber": 3,
    "transactionIndex": 0,
    "from": "0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b",
    "to": "0x6295ee1b4f6dd65047762f924ecd367c17eabf8f",
    "value": '123450000000000000',
    "gas": 314159,
    "gasPrice": '2000000000000',
    "input": "0x57cb2fc4"
}
```

***

### getPendingTransactions

```
web3.eth.getPendingTransactions([, callback])
```

Returns a list of pending transactions.

#### Parameters

1. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise<object[]>` - Array of pending transactions:

> * `hash` 32 Bytes - `String`: Hash of the transaction.
> * `nonce` - `Number`: The number of transactions made by the sender prior to this one.
> * `blockHash` 32 Bytes - `String`: Hash of the block where this transaction was in. `null` if pending.
> * `blockNumber` - `Number`: Block number where this transaction was in. `null` if pending.
> * `transactionIndex` - `Number`: Integer of the transactions index position in the block. `null` if pending.
> * `from` - `String`: Address of the sender.
> * `to` - `String`: Address of the receiver. `null` when it’s a contract creation transaction.
> * `value` - `String`: Value transferred in wei.
> * `gasPrice` - `String`: The wei per unit of gas provided by the sender in wei.
> * `gas` - `Number`: Gas provided by the sender.
> * `input` - `String`: The data sent along with the transaction.

#### Example

```
 web3.eth.getPendingTransactions().then(console.log);
 >  [
     {
         hash: '0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b',
         nonce: 2,
         blockHash: '0xef95f2f1ed3ca60b048b4bf67cde2195961e0bba6f70bcbea9a2c4e133e34b46',
         blockNumber: 3,
         transactionIndex: 0,
         from: '0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b',
         to: '0x6295ee1b4f6dd65047762f924ecd367c17eabf8f',
         value: '123450000000000000',
         gas: 314159,
         gasPrice: '2000000000000',
         input: '0x57cb2fc4'
         v: '0x3d',
         r: '0xaabc9ddafffb2ae0bac4107697547d22d9383667d9e97f5409dd6881ce08f13f',
         s: '0x69e43116be8f842dcd4a0b2f760043737a59534430b762317db21d9ac8c5034'
     },....,{
         hash: '0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b',
         nonce: 3,
         blockHash: '0xef95f2f1ed3ca60b048b4bf67cde2195961e0bba6f70bcbea9a2c4e133e34b46',
         blockNumber: 4,
         transactionIndex: 0,
         from: '0xa94f5374fce5edbc8e2a8697c15331677e6ebf0b',
         to: '0x6295ee1b4f6dd65047762f924ecd367c17eabf8f',
         value: '123450000000000000',
         gas: 314159,
         gasPrice: '2000000000000',
         input: '0x57cb2fc4'
         v: '0x3d',
         r: '0xaabc9ddafffb2ae0bac4107697547d22d9383667d9e97f5409dd6881ce08f13f',
         s: '0x69e43116be8f842dcd4a0b2f760043737a59534430b762317db21d9ac8c5034'
     }
]
```

***

### getTransactionFromBlock

```
getTransactionFromBlock(hashStringOrNumber, indexNumber [, callback])
```

Returns a transaction based on a block hash or number and the transaction’s index position.

#### Parameters

1. `String|Number|BN|BigNumber` - A block number or hash. Or the string `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` as in the [default block parameter](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock).
2. `Number` - The transaction’s index position.
3. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Object` - A transaction object, see [web3.eth.getTransaction](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-gettransaction-return):

#### Example

```
var transaction = web3.eth.getTransactionFromBlock('0x4534534534', 2)
.then(console.log);
> // see web3.eth.getTransaction
```

***

### getTransactionReceipt

```
web3.eth.getTransactionReceipt(hash [, callback])
```

Returns the receipt of a transaction by transaction hash.

Note

The receipt is not available for pending transactions and returns `null`.

#### Parameters

1. `String` - The transaction hash.
2. `String` - (optional) The `hex` keyword can be passed as second argument, in order to format in hex, values that would be `Number` otherwise.
3. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Object` - A transaction receipt object, or `null` if no receipt was found:

> * `status` - `Boolean`: `TRUE` if the transaction was successful, `FALSE` if the EVM reverted the transaction.
> * `blockHash` 32 Bytes - `String`: Hash of the block where this transaction was in.
> * `blockNumber` - `Number` (or `hex String`): Block number where this transaction was in.
> * `transactionHash` 32 Bytes - `String`: Hash of the transaction.
> * `transactionIndex`- `Number` (or `hex String`): Integer of the transactions index position in the block.
> * `from` - `String`: Address of the sender.
> * `to` - `String`: Address of the receiver. `null` when it’s a contract creation transaction.
> * `contractAddress` - `String`: The contract address created, if the transaction was a contract creation, otherwise `null`.
> * `cumulativeGasUsed` - `Number` (or `hex String`): The total amount of gas used when this transaction was executed in the block.
> * `gasUsed` - `Number` (or `hex String`): The amount of gas used by this specific transaction alone.
> * `logs` - `Array`: Array of log objects, which this transaction generated.
> * `effectiveGasPrice` - `Number` (or `hex String`): The actual value per gas deducted from the senders account. Before EIP-1559, this is equal to the transaction’s gas price. After, it is equal to baseFeePerGas + min(maxFeePerGas - baseFeePerGas, maxPriorityFeePerGas).

#### Example

```
var receipt = web3.eth.getTransactionReceipt('0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b')
.then(console.log);

> {
  "status": true,
  "transactionHash": "0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b",
  "transactionIndex": 0,
  "blockHash": "0xef95f2f1ed3ca60b048b4bf67cde2195961e0bba6f70bcbea9a2c4e133e34b46",
  "blockNumber": 3,
  "contractAddress": "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe",
  "cumulativeGasUsed": 314159,
  "gasUsed": 30234,
  "logs": [{
         // logs as returned by getPastLogs, etc.
     }, ...]
}

var receipt = web3.eth.getTransactionReceipt('0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b','hex')
.then(console.log);
> {
  "status": true,
  "transactionHash": "0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b",
  "transactionIndex": '0x0',
  "blockHash": "0xef95f2f1ed3ca60b048b4bf67cde2195961e0bba6f70bcbea9a2c4e133e34b46",
  "blockNumber": '0x3',
  "contractAddress": "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe",
  "cumulativeGasUsed": '0x4cb2f',
  "gasUsed": '0x761a',
  "logs": [{
         // logs as returned by getPastLogs, etc.
     }, ...]
}
```

***

### getTransactionCount

```
web3.eth.getTransactionCount(address [, defaultBlock] [, callback])
```

Get the number of transactions sent from this address.

#### Parameters

1. `String` - The address to get the numbers of transactions from.
2. `Number|String|BN|BigNumber` - (optional) If you pass this parameter it will not use the default block set with [web3.eth.defaultBlock](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock). Pre-defined block numbers as `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` can also be used.
3. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Number` - The number of transactions sent from the given address.

#### Example

```
web3.eth.getTransactionCount("0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe")
.then(console.log);
> 1
```

***

### sendTransaction

```
web3.eth.sendTransaction(transactionObject [, callback])
```

Sends a transaction to the network.

#### Parameters

1. `Object` - The transaction object to send:
   * `from` - `String|Number`: The address for the sending account. Uses the web3.eth.defaultAccount property, if not specified. Or an address or index of a local wallet in web3.eth.accounts.wallet.
   * `to` - `String`: (optional) The destination address of the message, left undefined for a contract-creation transaction.
   * `value` - `Number|String|BN|BigNumber`: (optional) The value transferred for the transaction in wei, also the endowment if it’s a contract-creation transaction.
   * `gas` - `Number`: (optional, default: To-Be-Determined) The amount of gas to use for the transaction (unused gas is refunded).
   * `gasPrice` - `Number|String|BN|BigNumber`: (optional) The price of gas for this transaction in wei, defaults to [web3.eth.gasPrice](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-gasprice).
   * `type` - `Number|String|BN|BigNumber`: (optional) A positive unsigned 8-bit number between 0 and 0x7f that represents the type of the transaction.
   * `maxFeePerGas` - `Number|String|BN`: (optional, defaulted to `(2 * block.baseFeePerGas) + maxPriorityFeePerGas`) The maximum fee per gas that the transaction is willing to pay in total
   * `maxPriorityFeePerGas` - `Number|String|BN` (optional, defaulted to `2.5 Gwei`) The maximum fee per gas to give miners to incentivize them to include the transaction (Priority fee)
   * `accessList` - `List of hexstrings` (optional) a list of addresses and storage keys that the transaction plans to access
   * `data` - `String`: (optional) Either a [ABI byte string](http://solidity.readthedocs.io/en/latest/abi-spec.html) containing the data of the function call on a contract, or in the case of a contract-creation transaction the initialisation code.
   * `nonce` - `Number`: (optional) Integer of the nonce. This allows to overwrite your own pending transactions that use the same nonce.
   * `chain` - `String`: (optional) Defaults to `mainnet`.
   * `hardfork` - `String`: (optional) Defaults to `london`.
   * `common` - `Object`: (optional) The common object
     * `customChain` - `Object`: The custom chain properties
       * `name` - `string`: (optional) The name of the chain
       * `networkId` - `number`: Network ID of the custom chain
       * `chainId` - `number`: Chain ID of the custom chain
     * `baseChain` - `string`: (optional) `mainnet`, `goerli`, `kovan`, `rinkeby`, or `ropsten`
     * `hardfork` - `string`: (optional) `chainstart`, `homestead`, `dao`, `tangerineWhistle`, `spuriousDragon`, `byzantium`, `constantinople`, `petersburg`, `istanbul`, `berlin`, or `london`
2. `callback` - `Function`: (optional) Optional callback, returns an error object as first parameter and the result as second.

Note

The `from` property can also be an address or index from the web3.eth.accounts.wallet. It will then sign locally using the private key of that account, and send the transaction via [web3.eth.sendSignedTransaction()](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-sendsignedtransaction). If the properties `chain` and `hardfork` or `common` are not set, Web3 will try to set appropriate values by querying the network for its chainId and networkId.

#### Returns

The **callback** will return the 32 bytes transaction hash.

`PromiEvent`: A [promise combined event emitter](https://web3js.readthedocs.io/en/v1.8.2/callbacks-promises-events.html#promievent). Resolves when the transaction [receipt](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-gettransactionreceipt-return) is available. The following events are also available:

* `sending` returns `payload: Object`: Fired immediately before transmitting the transaction request.
* `sent` returns `payload: Object`: Fired immediately after the request body has been written to the client, but before the transaction hash is received.
* `"transactionHash"` returns `transactionHash: String`: Fired when the transaction hash is available.
* `"receipt"` returns `receipt: Object`: Fired when the transaction receipt is available.
* `"confirmation"` returns `confirmationNumber: Number`, `receipt: Object`, `latestBlockHash: String`: Fired for every confirmation up to the 12th confirmation. Receives the confirmation number as the first and the [receipt](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-gettransactionreceipt-return) as the second argument. Fired from confirmation 0 on, which is the block where it’s mined.

`"error"` returns `error: Error`: Fired if an error occurs during sending. If the transaction was rejected by the network with a receipt, the receipt will be available as a property on the error object.

#### Example

```
// compiled solidity source code using https://remix.ethereum.org
var code = "603d80600c6000396000f3007c01000000000000000000000000000000000000000000000000000000006000350463c6888fa18114602d57005b6007600435028060005260206000f3";


// using the callback
web3.eth.sendTransaction({
    from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe',
    data: code // deploying a contract
}, function(error, hash){
    ...
});

// using the promise
web3.eth.sendTransaction({
    from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe',
    to: '0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe',
    value: '1000000000000000'
})
.then(function(receipt){
    ...
});


// using the event emitter
web3.eth.sendTransaction({
    from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe',
    to: '0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe',
    value: '1000000000000000'
})
.on('transactionHash', function(hash){
    ...
})
.on('receipt', function(receipt){
    ...
})
.on('confirmation', function(confirmationNumber, receipt){ ... })
.on('error', console.error); // If a out of gas error, the second parameter is the receipt.
```

***

### sendSignedTransaction

```
web3.eth.sendSignedTransaction(signedTransactionData [, callback])
```

Sends an already signed transaction, generated for example using [web3.eth.accounts.signTransaction](https://web3js.readthedocs.io/en/v1.8.2/web3-eth-accounts.html#eth-accounts-signtransaction).

#### Parameters

1. `String` - Signed transaction data in HEX format
2. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`PromiEvent`: A [promise combined event emitter](https://web3js.readthedocs.io/en/v1.8.2/callbacks-promises-events.html#promievent). Resolves when the transaction [receipt](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-gettransactionreceipt-return) is available.

Please see the return values for [web3.eth.sendTransaction](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-sendtransaction-return) for details.

#### Example

```
var Tx = require('@ethereumjs/tx').Transaction;
var privateKey = Buffer.from('e331b6d69882b4cb4ea581d88e0b604039a3de5967688d3dcffdd2270c0fd109', 'hex');

var rawTx = {
  nonce: '0x00',
  gasPrice: '0x09184e72a000',
  gasLimit: '0x2710',
  to: '0x0000000000000000000000000000000000000000',
  value: '0x00',
  data: '0x7f7465737432000000000000000000000000000000000000000000000000000000600057'
}

var tx = new Tx(rawTx, {'chain':'ropsten'});
var signedTx = tx.sign(privateKey);

var serializedTx = signedTx.serialize();

// console.log(serializedTx.toString('hex'));
// 0xf889808609184e72a00082271094000000000000000000000000000000000000000080a47f74657374320000000000000000000000000000000000000000000000000000006000571ca08a8bbf888cfa37bbf0bb965423625641fc956967b81d12e23709cead01446075a01ce999b56a8a88504be365442ea61239198e23d1fce7d00fcfc5cd3b44b7215f

web3.eth.sendSignedTransaction('0x' + serializedTx.toString('hex'))
.on('receipt', console.log);

> // see eth.getTransactionReceipt() for details
```

Note

When using _ethereumjs-tx@2.0.0_ if you don’t specify the parameter _chain_ it will use _mainnet_ by default.

***

### sign

```
web3.eth.sign(dataToSign, address [, callback])
```

Signs data using a specific account. This account needs to be unlocked.

#### Parameters

1. `String` - Data to sign. If it is a string it will be converted using [web3.utils.utf8ToHex](https://web3js.readthedocs.io/en/v1.8.2/web3-utils.html#utils-utf8tohex).
2. `String|Number` - Address to sign data with. Can be an address or the index of a local wallet in web3.eth.accounts.wallet.
3. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `String` - The signature.

#### Example

```
web3.eth.sign("Hello world", "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe")
.then(console.log);
> "0x30755ed65396facf86c53e6217c52b4daebe72aa4941d89635409de4c9c7f9466d4e9aaec7977f05e923889b33c0d0dd27d7226b6e6f56ce737465c5cfd04be400"

// the below is the same
web3.eth.sign(web3.utils.utf8ToHex("Hello world"), "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe")
.then(console.log);
> "0x30755ed65396facf86c53e6217c52b4daebe72aa4941d89635409de4c9c7f9466d4e9aaec7977f05e923889b33c0d0dd27d7226b6e6f56ce737465c5cfd04be400"
```

***

### signTransaction

```
web3.eth.signTransaction(transactionObject, address [, callback])
```

Signs a transaction. This account needs to be unlocked.

#### Parameters

1. `Object` - The transaction data to sign. See [web3.eth.sendTransaction()](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-sendtransaction) for more.
2. `String` - Address to sign transaction with.
3. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Object` - The RLP encoded transaction. The `raw` property can be used to send the transaction using [web3.eth.sendSignedTransaction](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-sendsignedtransaction).

#### Example

```
web3.eth.signTransaction({
    from: "0xEB014f8c8B418Db6b45774c326A0E64C78914dC0",
    gasPrice: "20000000000",
    gas: "21000",
    to: '0x3535353535353535353535353535353535353535',
    value: "1000000000000000000",
    data: ""
}).then(console.log);
> {
    raw: '0xf86c808504a817c800825208943535353535353535353535353535353535353535880de0b6b3a76400008025a04f4c17305743700648bc4f6cd3038ec6f6af0df73e31757007b7f59df7bee88da07e1941b264348e80c78c4027afc65a87b0a5e43e86742b8ca0823584c6788fd0',
    tx: {
        nonce: '0x0',
        gasPrice: '0x4a817c800',
        gas: '0x5208',
        to: '0x3535353535353535353535353535353535353535',
        value: '0xde0b6b3a7640000',
        input: '0x',
        v: '0x25',
        r: '0x4f4c17305743700648bc4f6cd3038ec6f6af0df73e31757007b7f59df7bee88d',
        s: '0x7e1941b264348e80c78c4027afc65a87b0a5e43e86742b8ca0823584c6788fd0',
        hash: '0xda3be87732110de6c1354c83770aae630ede9ac308d9f7b399ecfba23d923384'
    }
}
```

***

### call

```
web3.eth.call(callObject [, defaultBlock] [, callback])
```

Executes a message call transaction, which is directly executed in the VM of the node, but never mined into the blockchain.

#### Parameters

1. `Object` - A transaction object, see [web3.eth.sendTransaction](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-sendtransaction-return). For calls the `from` property is optional however it is highly recommended to explicitly set it or it may default to _address(0)_ depending on your node or provider.
2. `Number|String|BN|BigNumber` - (optional) If you pass this parameter it will not use the default block set with [web3.eth.defaultBlock](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock). Pre-defined block numbers as `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` can also be used.
3. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `String`: The returned data of the call, e.g. a smart contract functions return value.

#### Example

```
web3.eth.call({
    to: "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe", // contract address
    data: "0xc6888fa10000000000000000000000000000000000000000000000000000000000000003"
})
.then(console.log);
> "0x000000000000000000000000000000000000000000000000000000000000000a"
```

***

### estimateGas

```
web3.eth.estimateGas(callObject [, callback])
```

Executes a message call or transaction and returns the amount of the gas used. Note: You must specify a `from` address otherwise you may experience odd behavior.

#### Parameters

1. `Object` - A transaction object, see [web3.eth.sendTransaction](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-sendtransaction-return) with the difference that for calls the `from` property is optional as well.
2. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Number` - the used gas for the simulated call/transaction.

#### Example

```
web3.eth.estimateGas({
    to: "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe",
    data: "0xc6888fa10000000000000000000000000000000000000000000000000000000000000003"
})
.then(console.log);
> "0x0000000000000000000000000000000000000000000000000000000000000015"
```

***

### getPastLogs

```
web3.eth.getPastLogs(options [, callback])
```

Gets past logs, matching the given options.

#### Parameters

1. `Object` - The filter options as follows:

> * `fromBlock` - `Number|String`: The number of the earliest block (or any of block tag `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` can also be used). By default `"latest"`.
> * `toBlock` - `Number|String`: The number of the latest block (or any of block tag `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` can also be used). By default `"latest"`.
> * `address` - `String|Array`: An address or a list of addresses to only get logs from particular account(s).
> * `topics` - `Array`: An array of values which must each appear in the log entries. The order is important, if you want to leave topics out use `null`, e.g. `[null, '0x12...']`. You can also pass an array for each topic with options for that topic e.g. `[null, ['option1', 'option2']]`

#### Returns

`Promise` returns `Array` - Array of log objects.

The structure of the returned event `Object` in the `Array` looks as follows:

* `address` - `String`: From which this event originated from.
* `data` - `String`: The data containing non-indexed log parameter.
* `topics` - `Array`: An array with max 4 32 Byte topics, topic 1-3 contains indexed parameters of the log.
* `logIndex` - `Number`: Integer of the event index position in the block.
* `transactionIndex` - `Number`: Integer of the transaction’s index position, the event was created in.
* `transactionHash` 32 Bytes - `String`: Hash of the transaction this event was created in.
* `blockHash` 32 Bytes - `String`: Hash of the block where this event was created in. `null` if still pending.
* `blockNumber` - `Number`: The block number where this log was created in. `null` if still pending.

#### Example

```
web3.eth.getPastLogs({
    address: "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe",
    topics: ["0x033456732123ffff2342342dd12342434324234234fd234fd23fd4f23d4234"]
})
.then(console.log);

> [{
    data: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
    topics: ['0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7', '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385']
    logIndex: 0,
    transactionIndex: 0,
    transactionHash: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
    blockHash: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    blockNumber: 1234,
    address: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'
},{...}]
```

***

### getWork

```
web3.eth.getWork([callback])
```

Gets work for miners to mine on. Returns the hash of the current block, the seedHash, and the boundary condition to be met (“target”).

#### Parameters

1. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Array` - the mining work with the following structure:

> * `String` 32 Bytes - at **index 0**: current block header pow-hash
> * `String` 32 Bytes - at **index 1**: the seed hash used for the DAG.
> * `String` 32 Bytes - at **index 2**: the boundary condition (“target”), 2^256 / difficulty.

#### Example

```
web3.eth.getWork()
.then(console.log);
> [
  "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
  "0x5EED00000000000000000000000000005EED0000000000000000000000000000",
  "0xd1ff1c01710000000000000000000000d1ff1c01710000000000000000000000"
]
```

***

### submitWork

```
web3.eth.submitWork(nonce, powHash, digest, [callback])
```

Used for submitting a proof-of-work solution.

#### Parameters

1. `String` 8 Bytes: The nonce found (64 bits)
2. `String` 32 Bytes: The header’s pow-hash (256 bits)
3. `String` 32 Bytes: The mix digest (256 bits)
4. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise` returns `Boolean` - Returns `TRUE` if the provided solution is valid, otherwise `FALSE`.

#### Example

```
web3.eth.submitWork([
    "0x0000000000000001",
    "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
    "0xD1FE5700000000000000000000000000D1FE5700000000000000000000000000"
])
.then(console.log);
> true
```

***

### requestAccounts

```
web3.eth.requestAccounts([callback])
```

This method will request/enable the accounts from the current environment. This method will only work if you’re using the injected provider from a application like Metamask, Status or TrustWallet. It doesn’t work if you’re connected to a node with a default Web3.js provider (WebsocketProvider, HttpProvider and IpcProvider).

For more information about the behavior of this method please read [EIP-1102: Opt-in account exposure](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1102.md).

#### Parameters

1. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise<Array>` - Returns an array of enabled accounts.

#### Example

```
web3.eth.requestAccounts().then(console.log);
> ['0aae0B295369a9FD31d5F28D9Ec85E40f4cb692BAf', '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe']
```

***

### getChainId

```
web3.eth.getChainId([callback])
```

Returns the chain ID of the current connected node as described in the [EIP-695](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-695.md).

#### Returns

`Promise<Number>` - Returns chain ID.

#### Example

```
web3.eth.getChainId().then(console.log);
> 61
```

***

### getNodeInfo

```
web3.eth.getNodeInfo([callback])
```

#### Returns

`Promise<String>` - The current client version.

#### Example

```
web3.eth.getNodeInfo().then(console.log);
> "Mist/v0.9.3/darwin/go1.4.1"
```

***

### getProof

```
web3.eth.getProof(address, storageKey, blockNumber, [callback])
```

Returns the account and storage-values of the specified account including the Merkle-proof as described in [EIP-1186](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1186.md).

#### Parameters

1. `String` 20 Bytes: The Address of the account or contract.
2. `Number[] | BigNumber[] | BN[] | String[]` 32 Bytes: Array of storage-keys which should be proofed and included. See web3.eth.getStorageAt.
3. `Number | String | BN | BigNumber`: Integer block number. Pre-defined block numbers as `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` can also be used.
4. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

#### Returns

`Promise<Object>` - A account object.

> * `address` - `String`: The address of the account.
> * `balance` - `String`: The balance of the account. See web3.eth.getBalance.
> * `codeHash` - `String`: hash of the code of the account. For a simple account without code it will return `"0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470"`.
> * `nonce` - `String`: Nonce of the account.
> * `storageHash` - `String`: SHA3 of the StorageRoot. All storage will deliver a MerkleProof starting with this rootHash.
> * `accountProof` - `String[]`:Array of rlp-serialized MerkleTree-Nodes, starting with the stateRoot-Node, following the path of the SHA3 (address) as key.
> * `storageProof` - `Object[]` Array of storage-entries as requested.
>   * `key` - `String` The requested storage key.
>   * `value` - `String` The storage value.

#### Example

```
web3.eth.getProof(
    "0x1234567890123456789012345678901234567890",
    ["0x0000000000000000000000000000000000000000000000000000000000000000","0x0000000000000000000000000000000000000000000000000000000000000001"],
    "latest"
).then(console.log);
> {
    "address": "0x1234567890123456789012345678901234567890",
    "accountProof": [
        "0xf90211a090dcaf88c40c7bbc95a912cbdde67c175767b31173df9ee4b0d733bfdd511c43a0babe369f6b12092f49181ae04ca173fb68d1a5456f18d20fa32cba73954052bda0473ecf8a7e36a829e75039a3b055e51b8332cbf03324ab4af2066bbd6fbf0021a0bbda34753d7aa6c38e603f360244e8f59611921d9e1f128372fec0d586d4f9e0a04e44caecff45c9891f74f6a2156735886eedf6f1a733628ebc802ec79d844648a0a5f3f2f7542148c973977c8a1e154c4300fec92f755f7846f1b734d3ab1d90e7a0e823850f50bf72baae9d1733a36a444ab65d0a6faaba404f0583ce0ca4dad92da0f7a00cbe7d4b30b11faea3ae61b7f1f2b315b61d9f6bd68bfe587ad0eeceb721a07117ef9fc932f1a88e908eaead8565c19b5645dc9e5b1b6e841c5edbdfd71681a069eb2de283f32c11f859d7bcf93da23990d3e662935ed4d6b39ce3673ec84472a0203d26456312bbc4da5cd293b75b840fc5045e493d6f904d180823ec22bfed8ea09287b5c21f2254af4e64fca76acc5cd87399c7f1ede818db4326c98ce2dc2208a06fc2d754e304c48ce6a517753c62b1a9c1d5925b89707486d7fc08919e0a94eca07b1c54f15e299bd58bdfef9741538c7828b5d7d11a489f9c20d052b3471df475a051f9dd3739a927c89e357580a4c97b40234aa01ed3d5e0390dc982a7975880a0a089d613f26159af43616fd9455bb461f4869bfede26f2130835ed067a8b967bfb80",
        "0xf90211a0395d87a95873cd98c21cf1df9421af03f7247880a2554e20738eec2c7507a494a0bcf6546339a1e7e14eb8fb572a968d217d2a0d1f3bc4257b22ef5333e9e4433ca012ae12498af8b2752c99efce07f3feef8ec910493be749acd63822c3558e6671a0dbf51303afdc36fc0c2d68a9bb05dab4f4917e7531e4a37ab0a153472d1b86e2a0ae90b50f067d9a2244e3d975233c0a0558c39ee152969f6678790abf773a9621a01d65cd682cc1be7c5e38d8da5c942e0a73eeaef10f387340a40a106699d494c3a06163b53d956c55544390c13634ea9aa75309f4fd866f312586942daf0f60fb37a058a52c1e858b1382a8893eb9c1f111f266eb9e21e6137aff0dddea243a567000a037b4b100761e02de63ea5f1fcfcf43e81a372dafb4419d126342136d329b7a7ba032472415864b08f808ba4374092003c8d7c40a9f7f9fe9cc8291f62538e1cc14a074e238ff5ec96b810364515551344100138916594d6af966170ff326a092fab0a0d31ac4eef14a79845200a496662e92186ca8b55e29ed0f9f59dbc6b521b116fea090607784fe738458b63c1942bba7c0321ae77e18df4961b2bc66727ea996464ea078f757653c1b63f72aff3dcc3f2a2e4c8cb4a9d36d1117c742833c84e20de994a0f78407de07f4b4cb4f899dfb95eedeb4049aeb5fc1635d65cf2f2f4dfd25d1d7a0862037513ba9d45354dd3e36264aceb2b862ac79d2050f14c95657e43a51b85c80",
        "0xf90171a04ad705ea7bf04339fa36b124fa221379bd5a38ffe9a6112cb2d94be3a437b879a08e45b5f72e8149c01efcb71429841d6a8879d4bbe27335604a5bff8dfdf85dcea00313d9b2f7c03733d6549ea3b810e5262ed844ea12f70993d87d3e0f04e3979ea0b59e3cdd6750fa8b15164612a5cb6567cdfb386d4e0137fccee5f35ab55d0efda0fe6db56e42f2057a071c980a778d9a0b61038f269dd74a0e90155b3f40f14364a08538587f2378a0849f9608942cf481da4120c360f8391bbcc225d811823c6432a026eac94e755534e16f9552e73025d6d9c30d1d7682a4cb5bd7741ddabfd48c50a041557da9a74ca68da793e743e81e2029b2835e1cc16e9e25bd0c1e89d4ccad6980a041dda0a40a21ade3a20fcd1a4abb2a42b74e9a32b02424ff8db4ea708a5e0fb9a09aaf8326a51f613607a8685f57458329b41e938bb761131a5747e066b81a0a16808080a022e6cef138e16d2272ef58434ddf49260dc1de1f8ad6dfca3da5d2a92aaaadc58080",
        "0xf851808080a009833150c367df138f1538689984b8a84fc55692d3d41fe4d1e5720ff5483a6980808080808080808080a0a319c1c415b271afc0adcb664e67738d103ac168e0bc0b7bd2da7966165cb9518080"
    ],
    "balance": 0,
    "codeHash": "0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
    "nonce": 0,
    "storageHash": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
    "storageProof": [
        {
            "key": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "value": '0',
            "proof": []
        },
        {
            "key": "0x0000000000000000000000000000000000000000000000000000000000000001",
            "value": '0',
            "proof": []
        }
    ]
}
```

***

### createAccessList

```
web3.eth.createAccessList(callObject [, callback])
```

Will call to create an access list a method execution will access when executed in the EVM. Note: Currently _eth\_createAccessList_ seems to only be supported by Geth. Note: You must specify a `from` address and `gas` if it’s not specified in `options` when instantiating parent contract object (e.g. `new web3.eth.Contract(jsonInterface[, address][, options])`).

#### Parameters

1. A transaction object, see [web3.eth.sendTransaction](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-sendtransaction-return) with the difference that this method is specifically for contract method executions.
2. `block` - `String|Number|BN|BigNumber` (optional): The block number or hash. Or the string `"earliest"`, `"latest"` , `"pending"`, `"safe"` or `"finalized"` as in the [default block parameter](https://web3js.readthedocs.io/en/v1.8.2/web3-eth.html#eth-defaultblock).
3. `callback` - `Function` (optional): This callback will be fired with the result of the access list generation as the second argument, or with an error object as the first argument.

#### Returns

`Promise` returns `Object`: The generated access list for transaction.

```
{
    "accessList": [
        {
            "address": "0x00f5f5f3a25f142fafd0af24a754fafa340f32c7",
            "storageKeys": [
                "0x0000000000000000000000000000000000000000000000000000000000000000"
            ]
        }
    ],
    "gasUsed": "0x644e"
}
```

#### Example

```
web3.eth.createAccessList({
    from: '0x3bc5885c2941c5cda454bdb4a8c88aa7f248e312',
    data: '0x20965255',
    gasPrice: '0x3b9aca00',
    gas: '0x3d0900',
    to: '0x00f5f5f3a25f142fafd0af24a754fafa340f32c7'
})
.then(console.log);
```

