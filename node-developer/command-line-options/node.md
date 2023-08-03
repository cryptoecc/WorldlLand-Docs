# Node

ETH-ECC 노드는 월드랜드 네트워크에 연결되어 월드랜드 네트워크의 최신 상태를 따라잡기 위해 동기화합니다. 서로 다른 메커니즘을 사용하여 체인의 헤드까지 동기화하는 두 가지 유형의 노드 방식과 두 가지 유형의 동기화 방식이 존재합니다.



## **Node**

### Full Node(default) <a href="#summary" id="summary"></a>

The basic node method is the Full Node method. The main feature of full nodes is to save storage space by maintaining the state of 128 blocks at the latest block height and removing past state data. It removes past state data, but keeps checkpoints from which state data can be recreated. If you need historical data from the past, you can recreate it with checkpoints. The full node approach effectively saves storage space, but is inefficient when fast querying of historical data is required.

```
$ ./worldland -gcmode full
```

### Archive node

The archive node does not remove all historical data, it retains it by itself. All data is directly accessible from the node itself, so there is no need to regenerate data with checkpoints. Since the node owns all blockchain data, it is a true blockchain node. However, since Archivenode takes up a lot of disk space, it is not suitable for all users.

```
$ ./worldland -gcmode archive
```

| Full Node | Archive Node |
| :-------: | :----------: |
|           |              |
|           |              |
|           |              |

### Hardware Requirements(2023-08-08)

**Full Node:**

* CPU with 2+ cores
* 4GB RAM
* 500GB free storage space to sync the Mainnet
* 8 MBit/sec download Internet service

**Archive Node:**

* Fast CPU with 4+ cores
* 16GB+ RAM
* High-performance SSD with at least 1TB of free space
* 25+ MBit/sec download Internet service

##

## **Sync Mode**

### Snap(default)

Snap sync starts with a relatively recent block and syncs to the head of the chain, keeping only the most recent **128 block** states in memory. Between the initial sync block and the most recent 128 blocks, nodes save intermittent snapshots that can be used to rebuild intermediate states "on the fly". The **difference** between a **snap sync** node and a **full block-by-block sync** node is that a **snap sync** node starts at an initial checkpoint that is more recent than the genesis block. Snap sync is much faster than Genesis' full block-by-block sync. To start the node with snap sync, pass on startup.

```
$ ./worldland -syncmode snap
```

### Full

Full block-by-block synchronization starts with the **genesis block** and executes all blocks to create the current state. Full sync re-executes transactions across the entire historical sequence of blocks to independently verify block origins and all state transitions. Only the most recent 128 block states are stored across all nodes. Stale block states are periodically pruned and marked as a series of checkpoints from which old states can be recreated on demand. 128 blocks is a record of about 25.6 minutes with a block time of 12 seconds.

```
$ ./worldland -syncmode full
```

| Full Sync | Snap Sync |
| --------- | --------- |
|           |           |
|           |           |
|           |           |

{% hint style="info" %}
We outline both types of full nodes and guides for getting them up and running. For a detailed description of the node, please refer to the following[ **link**](https://geth.ethereum.org/docs/fundamentals/sync-modes).
{% endhint %}









### &#x20;<a href="#archive-nodes" id="archive-nodes"></a>





### Sync Mode





### &#x20;<a href="#summary" id="summary"></a>
