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

