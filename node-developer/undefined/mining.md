# Mining



The **WorldLand** blockchain is a proof-of-work blockchain. Nodes in **WorldLand** compete by running a specific algorithm called **ECCPoW**. The node that solved the algorithm the fastest creates and propagates the block. Other nodes verify that the received block actually solved the algorithm and accept the block only if it is verified. The series of processes that solve proof-of-work algorithms and generate blocks is called mining. ETH-ECC supports **CPU mining** of **ECCPoW** via the built-in miner.



### Start mining

Even when the ETH-ECC node starts, it does not mine by default. Mining requires direct setup. You can start a node as a miner with the `-mine` option.

```sh
$ ./worldland -mine
```



You can also start and stop mining while the node is running using the miner module in the JSON-RPC console.

You can start mining through the `miner.start()` command. If an integer is given as an input value, mining is executed with the corresponding number of threads.

```
> miner.start(4)
INFO [08-04|15:05:45.206] Updated mining threads                   threads=4
```

The `miner.stop()` command stops the node from mining.

```
> miner.stop()
null
```



### Syncing

If you proceed with mining without synchronizing the network, it is meaningless as it is the same as creating a new blockchain. Therefore, the ETH-ECC node delays mining until synchronization is complete, and mining proceeds automatically after synchronization and completion.&#x20;

Then, to check the sync progress in the console:

```sh
eth.syncing
```



If synchronization is in progress, the output is as follows.

```
> eth.syncing
{
  currentBlock: 13891665,
  healedBytecodeBytes: 0,
  healedBytecodes: 0,
  healedTrienodeBytes: 0,
  healedTrienodes: 0,
  healingBytecode: 0,
  healingTrienodes: 0,
  highestBlock: 14640000,
  startingBlock: 13891665,
  syncedAccountBytes: 0,
  syncedAccounts: 0,
  syncedBytecodeBytes: 0,
  syncedBytecodes: 0,
  syncedStorage: 0,
  syncedStorageBytes: 0
}
```



When sync returns false, sync is all done.

```
> eth.syncing
false
```



### Etherbase

You need to set up an etherbase account to be recorded as a miner. The etherbase account defaults to being the first account in eth.accounts , which is a node's account.set. However, you can set it to an alternate address using the -miner.etherbase command.

<pre class="language-sh"><code class="lang-sh"><strong>$ ./worldland -miner.etherbase 'YOUR_ACCOUNT' -mine
</strong></code></pre>

If no account is available, an account will be created automatically and set to Etherbase. You can manually change the etherbase using the console's minor module. etherbase does not have to be included on the local node, existing accounts are fine.

```sh
miner.setEtherbase(eth.accounts[2])
```



### Additional tips

Data can be stored by adding additional data (32 bytes) to the mined block. It is usually decoded to Unicode, so you can add any data you want to the block via the miner.setExtra() command in the console.

```sh
miner.setExtra("worldland")
```

You can also check the current hash rate in hash operations per second (H/s) using the console.

```sh
eth.hashrate
 712000
```

You can check the increased account balance through mining through the eth,getBalance() command.

```sh
eth.getBalance(eth.coinbase).toNumber();
 '34698870000000'
```



It may fluctuate after the balance increases. Even if it is the first block in the local blockchain, it can be reconstructed because there are earlier blocks that have not yet been propagated. When the chain is reconstructed, the blocks you create will not be included and block rewards will not be applied. The deeper the blocks generated, the safer they become. Logs only show mined blocks that are 7 block deep or higher to reduce balance indiscriminate fluctuations.

```
INFO [08-04|15:38:40.370] 🔗 block reached canonical chain          number=31720 hash=aaf485..dd2528
INFO [08-04|15:38:40.370] 🔨 mined potential block                  number=31727 hash=51968c..ba14fb
```



### &#x20;<a href="#summary" id="summary"></a>
