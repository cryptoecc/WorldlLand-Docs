# Install and run geth

### 1. Environment

For Windows, please visit [Windows instruciton](https://github.com/cryptoecc/ETH-ECC/blob/master/docs/eccpow%20windows%20instuction/Windows%20install%20instruction.md) before start. ETH-ECC package uses the follow two environment

* Amazon Linux 2 Kernel 5.10 or Linux Ubuntu 18.04
* Go (version 1.17 or later) develope language

You can follow two step below to download ETH-ECC and install(build)

**1.1 Downloading**

You can download ETH-ECC by cloning ETH-ECC repository.

```
$ git clone https://github.com/cryptoecc/ETH-ECC
```

#### 1.2 Installation

For building ETH-ECC, it requires Go (version 1.18 or later). You can install them using following commands.

```
$ sudo apt update
$ sudo apt install snapd
$ sudo snap install go --classic
```

Then Go will be installed

Check version of Go (version 1.18 or later)

```
$ go verison
```

Once, dependencies are installed, You can install ETH-ECC using the following command.

```
$ make geth
```

or, to build the full suite of utilities:

```
$ make all
```



### 2. Running ETH-ECC and connecting to LVE mainnet

First, you'll need to make a directory to store block information. For example `ETHECC_TEST` directory. Then move to `/ETH-ECC/build/bin`, and follow this.

```
$ ./geth --lve --datadir [Your_own_storage] console
```

For example,

```
(EXAMPLE) $ ./geth --lve --datadir /home/Documents/ETHECC_TEST console
```

it returns data that looks like:

```
INFO [01-02|14:59:12.563] Starting Geth on Lve ... 
INFO [01-02|14:59:12.565] Maximum peer count                       ETH=50 LES=0 total=50
INFO [01-02|14:59:12.566] Smartcard socket not found, disabling    err="stat /run/pcscd/pcscd.comm: no such file or directory"
INFO [01-02|14:59:12.568] Set global gas cap                       cap=50,000,000
INFO [01-02|14:59:12.570] Allocated trie memory caches             clean=154.00MiB dirty=256.00MiB
INFO [01-02|14:59:12.570] Allocated cache and file handles         database=/home/lvminer-5/deok/TEST/ETHECC_TEST/geth/chaindata cache=512.00MiB handles=524,288
INFO [01-02|14:59:12.676] Opened ancient database                  database=/home/lvminer-5/deok/TEST/ETHECC_TEST/geth/chaindata/ancient/chain readonly=false
INFO [01-02|14:59:12.676] Disk storage enabled for ethash caches   dir=/home/lvminer-5/deok/TEST/ETHECC_TEST/geth/ethash count=3
INFO [01-02|14:59:12.676] Disk storage enabled for ethash DAGs     dir=/home/lvminer-5/.ethash count=2
INFO [01-02|14:59:12.676] Initialising Ethereum protocol           network=12345 dbversion=<nil>
INFO [01-02|14:59:12.677] Writing custom genesis block 
INFO [01-02|14:59:12.703] Persisted trie from memory database      nodes=354 size=50.23KiB time=2.70146ms gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
INFO [01-02|14:59:12.706]  
INFO [01-02|14:59:12.706] --------------------------------------------------------------------------------------------------------------------------------------------------------- 
INFO [01-02|14:59:12.706] Chain ID:  12345 (lve) 
...
```

You can check ChainID is 12345.

You are now connected to the LVE network!
