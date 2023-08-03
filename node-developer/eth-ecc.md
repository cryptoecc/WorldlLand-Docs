# ETH-ECC

### What is ETH-ECC ?

**ETH-ECC** 는 월드랜드의 공식 노드 클라이언트 입니다. 이것은 이더리움의 공식 노드 클라이언트인 **ethereum/go-ethereum** 의 포크 입니다.&#x20;

{% hint style="info" %}
Geth(go-ethereum)는 탈중앙화 웹으로 가는 관문인 [이더리움](https://ethereum.org/)의 [Go](https://go.dev/) 구현입니다. Geth는 최초의 이더리움 구현 중 하나였으며 가장 전투적으로 단련되고 테스트된 클라이언트였습니다.
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



