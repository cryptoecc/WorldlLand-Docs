# Node

**ETH-ECC nodes** connect to the WorldLand network and synchronize to keep up with the latest state of the WorldLand network. There are **two types** of **node method**s and two types of **synchronization methods** that use different mechanisms to synchronize up to the head of the chain.

## **Node**

### Full Node(default) <a href="#summary" id="summary"></a>

The basic node method is the **Full Node** method. The main feature of full nodes is to save storage space by maintaining the state of **128 blocks** at the latest block height and removing past state data. It removes past state data but keeps **checkpoints** from which state data can be recreated. If you need historical data, you can **recreate** it with checkpoints. The full node approach effectively **saves** storage space but is inefficient when fast querying of historical data is required.

```
$ ./worldland <other flags> -gcmode full
```

### Archive node

The archive node does not remove **all historical data**. It retains it by itself. All data is **directly accessible** from the node itself, so there is no need to regenerate data with checkpoints. Since the node owns all blockchain data, it is a true blockchain node. However, since Archive node takes up a **lot of disk space**, it is not suitable for all users.

```
$ ./worldland <other flags> -gcmode archive
```



**The key differences between an Archive Node and a Full Node:**

<table><thead><tr><th width="219"></th><th>Full Node</th><th>Archive Node</th></tr></thead><tbody><tr><td>Data Retention</td><td>Retains only the latest block data</td><td>Retains all block data</td></tr><tr><td>Data Storage Size</td><td>Relatively smaller</td><td>Very large</td></tr><tr><td>Synchronization Time</td><td>Comparatively shorter</td><td>Lengthy</td></tr><tr><td>Purpose</td><td>Transaction broadcasting and network security maintenance</td><td>Block exploration and historical data verification</td></tr><tr><td>Higher Storage Costs</td><td>No</td><td>Yes</td></tr></tbody></table>

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



## **Sync Mode**

### Snap(default)

Snap sync starts with a relatively recent block and syncs to the head of the chain, keeping only the most recent **128 block** states in memory. Between the initial sync block and the most recent 128 blocks, nodes save intermittent snapshots that can be used to rebuild intermediate states "on the fly". The **difference** between a **snap sync** node and a **full block-by-block sync** node is that a **snap sync** node starts at an initial checkpoint that is more recent than the genesis block. Snap sync is much faster than Genesis' full block-by-block sync. To start the node with snap sync, pass on startup.

```
$ ./worldland <other flags> -syncmode snap
```

### Full

Full block-by-block synchronization starts with the **genesis block** and executes all blocks to create the current state. Full sync re-executes transactions across the entire historical sequence of blocks to independently verify block origins and all state transitions. Only the most recent 128 block states are stored across all nodes. Stale block states are periodically pruned and marked as a series of checkpoints from which old states can be recreated on demand. **128 blocks** is a record of about **21.3 minutes** with a block time of 10 seconds.

```
$ ./worldland <other flags> -syncmode full
```

<table><thead><tr><th></th><th>Snap Sync</th><th>Full Sync</th><th data-hidden>Snap Sync</th><th data-hidden></th><th data-hidden></th><th data-hidden>Full sync</th></tr></thead><tbody><tr><td>Data Download Method</td><td>Download snapshot file and sync</td><td>Sequentially download all blocks for synchronization</td><td></td><td></td><td>Data Download Method</td><td>Sequentially download all blocks for synchronization</td></tr><tr><td>Download Time</td><td>Faster</td><td>Takes longer</td><td></td><td>Download Time</td><td>Download Time</td><td>Takes longer</td></tr><tr><td>Purpose</td><td>Useful for quickly syncing new nodes</td><td>Required to verify full network history.</td><td></td><td></td><td>Purpose</td><td>Required for accessing the entire network history</td></tr><tr><td>Network Load</td><td>Low</td><td>High</td><td></td><td></td><td>Network Load</td><td>High</td></tr></tbody></table>







### &#x20;<a href="#summary" id="summary"></a>
