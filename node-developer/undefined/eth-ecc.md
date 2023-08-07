# ETH-ECC

### [https://github.com/cryptoecc/ETH-ECC](https://github.com/cryptoecc/ETH-ECC)

### What is ETH-ECC?

**Ethereum Error-Correction Code(ETH-ECC)** is  WorldLand's official node client. \
This is a fork of [**ethereum/go-ethereum**](https://github.com/ethereum/go-ethereum), the official node client for Ethereum.

{% hint style="info" %}
Geth (go-Ethereum) is a [Go](https://go.dev/) implementation of [Ethereum](https://ethereum.org/). It is one of the original and most popular Ethereum clients.
{% endhint %}

When **ETH-ECC** runs, the computer acts as a **Worldland** **node** and connects to the Worldland network. The **Worldland network** operates according to the WorldLand blockchain protocol, which handles the transactions, deployment, and execution of smart contracts and includes an embedded computer known as the **EVM**.&#x20;

The nodes perform a **proof-of-work** algorithm known as **ECCPoW**, The first node that solves the problem creates a new block containing a list of transactions that must be executed. Blocks are broadcast to the WorldLand network, and each node verifies that block and adds it to the database.



### ETH-ECC Node Overview&#x20;

The **ETH-ECC** node has the following roles and functions.

* Consensus is reached by running the [**ECCPoW**](https://doi.org/10.48550/arXiv.2006.12306) consensus algorithm.&#x20;
* Create and propagate blocks.&#x20;
* Validates the propagated block and synchronizes the "state**"** of WorldLand.&#x20;
* Validate and process transactions.&#x20;
* Deploy and execute smart contracts.&#x20;
* Execute bytecode using EVM.



### Why run a node?

Running your node allows you to use Worldland in a truly private, self-sufficient, and trustless way. You don't have to trust the information you receive because you can verify the data directly using the **ETH-ECC** instance.



The following sections was prepared by referring to go-ethereum's official document. See [**go-ethereum's documentation**](https://geth.ethereum.org/docs) for more details.





