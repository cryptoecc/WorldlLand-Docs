# Run Node

### Running ETH-ECC and connecting to Worldland



명령어 옵션



If you're running a geth node for the first time, or if you've run a different version of Ethereum or a chain with a different network number, run the following to initialize your locally stored block data

```
$ rm -rf ~/.ethereum
```



First, you'll need to make a directory to store block information. For example, `ETHECC_TEST` directory. Then move to `/ETH-ECC/build/bin`, and follow this.



```
$ ./worldland --datadir "USER_DATA_DIR" console
```



it returns data that looks like:

```
INFO [07-24|07:41:11.823] Starting clinet on Worldland Seoul mainnet... 
INFO [07-24|07:41:11.825] Maximum peer count                       ETH=50 LES=0 total=50
...
INFO [07-24|07:41:11.863] --------------------------------------------------------------------------------------------------------------------------------------------------------- 
INFO [07-24|07:41:11.863] Chain ID:  103 (seoul) 
INFO [07-24|07:41:11.863] Consensus: Eccpow (proof-of-work) 
INFO [07-24|07:41:11.863]  
INFO [07-24|07:41:11.863] --------------------------------------------------------------------------------------------------------------------------------------------------------- 
...
INFO [07-24|07:41:11.865] Starting peer-to-peer node               instance=Worldland/v1.0.0-unstable-58ebea70-20230724/linux-amd64/go1.20.6
INFO [07-24|07:41:11.875] New local node record                    seq=1,690,184,471,874 id=120fa3704cf0c197 ip=127.0.0.1 udp=30303 tcp=30303
INFO [07-24|07:41:11.876] IPC endpoint opened                      url=/home/ubuntu/test0724/geth.ipc
INFO [07-24|07:41:11.876] Generated JWT secret                     path=/home/ubuntu/test0724/worldland/jwtsecret
INFO [07-24|07:41:11.876] Started P2P networking                   self=enode://b2025f8b4da969805bb7a421ddee9ce4b8dabf5448bac0f5f3443a14aaf3573dec66506c192e0db7a45c5bbed52d02cd8d063607431b4c33a1ea7018e625b3c1@127.0.0.1:30303
INFO [07-24|07:41:11.877] WebSocket enabled                        url=ws://127.0.0.1:8551
INFO [07-24|07:41:11.877] HTTP server started                      endpoint=127.0.0.1:8551 auth=true prefix= cors=localhost vhosts=localhost
WARN [07-24|07:41:11.924] Served eth_coinbase                      reqid=3 duration="24.828µs" err="etherbase must be explicitly specified"
Welcome to the Worldland JavaScript console!

instance: Worldland/v1.0.0-unstable-58ebea70-20230724/linux-amd64/go1.20.6
at block: 0 (Tue Jul 18 2023 03:00:00 GMT+0000 (UTC))
 datadir: /home/ubuntu/test0724
 modules: admin:1.0 debug:1.0 ecc:1.0 engine:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0

To exit, press ctrl-d or type exit
```

You can check ChainID is 103.

You are now connected to the Seoul main network!
