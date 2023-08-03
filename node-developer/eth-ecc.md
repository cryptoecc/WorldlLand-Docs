# ETH-ECC

### What is ETH-ECC ?

**ETH-ECC** is Worldland's official node client. This is a fork of **ethereum/go-ethereum**, the official node client for Ethereum.

{% hint style="info" %}
Geth (go-ethereum) is a [Go](https://go.dev/) implementation of [Ethereum](https://ethereum.org/). It is one of the original and most popular Ethereum clients.
{% endhint %}

When **ETH-ECC** is running, the computer acts as a Worldland node and connects to the Worldland network. The Worldland network operates according to the Worldland blockchain protocol, which handles the transactions, deployment and execution of smart contracts and includes an embedded computer known as the **EVM**. The nodes perform a proof-of-work algorithm known as **ECCPoW**, The first node that solved the problem creates a new block containing a list of transactions that need to be executed. Blocks are broadcast to the Worldland network, and each node verifies that block and adds it to the database.



### ETH-ECC Node Overview&#x20;

The ETH-ECC node has the following roles and functions.

* Consensus is reached by running the ECCPoW consensus algorithm.&#x20;
* Create and propagate blocks.&#x20;
* Validates the propagated block and synchronizes the state of Worldland.&#x20;
* Validate and process transactions.&#x20;
* Deploy and execute smart contracts.&#x20;
* Execute bytecode using EVM.



### Why run a node?

Running your own node allows you to use Worldland in a truly private, self-sufficient and trustless way. You don't have to trust the information you receive because you can verify the data directly using the **ETH-ECC** instance.



