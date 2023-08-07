# Command-line options

### Run ETH-ECC

**ETH-ECC** is primarily controlled using the **command line**. ETH-ECC is started using the `worldland` command. Stop it by pressing **ctrl-c**.

```
./worldland <flags>
```

You can configure ETH-ECC using **command line options** (**flags**). ETH-ECC also has sub-commands that can invoke functions such as console or blockchain import/export.

As an alternative to passing the numerous flags to the worldland binary, you can also pass a **configuration file** via:

```
$ ./worldland <other flags> --config /path/to/your_config.toml
```



### **Config File**

To get an idea of how the file should look, you can use the `dumpconfig` sub-command to export your existing configuration:

```
$ ./worldland <other flags> dumpconfig >> CONFIG_DIR
```

**Example:**

```
$ ./worldland <other flags> -gwangju dumpconfig -datadir /home/worldland/gwangju >> config.toml
```

**Return:**

**config. toml**

````
# Note: this config doesn't contain the genesis block.

[Eth]
NetworkId = 10395
SyncMode = "snap"
EthDiscoveryURLs = ["enrtree://AKA3AM6LPBYEUDMVNU3BSVQJ5AD45Y7YPOHJLEF6W26QOE4VTUDPE@all.gwangju.ethdisco.net"]
SnapDiscoveryURLs = ["enrtree://AKA3AM6LPBYEUDMVNU3BSVQJ5AD45Y7YPOHJLEF6W26QOE4VTUDPE@all.gwangju.ethdisco.net"]
NoPruning = false
NoPrefetch = false
TxLookupLimit = 2350000
LightPeers = 100
UltraLightFraction = 75
DatabaseCache = 512
DatabaseFreezer = ""
TrieCleanCache = 154
TrieCleanCacheJournal = "triecache"
TrieCleanCacheRejournal = 3600000000000
TrieDirtyCache = 256
TrieTimeout = 3600000000000
SnapshotCache = 102
Preimages = false
FilterLogCacheSize = 32
EnablePreimageRecording = false
RPCGasCap = 50000000
RPCEVMTimeout = 5000000000
RPCTxFeeCap = 1e+00

[Eth.Miner]
GasFloor = 0
GasCeil = 30000000
GasPrice = 1000000000
Recommit = 3000000000
Noverify = false

[Eth.Ethash]
CacheDir = "ethash"
CachesInMem = 2
CachesOnDisk = 3
CachesLockMmap = false
DatasetDir = "/root/.ethash"
DatasetsInMem = 1
DatasetsOnDisk = 2
DatasetsLockMmap = false
PowMode = 0
NotifyFull = false

[Eth.TxPool]
Locals = []
NoLocals = false
Journal = "transactions.rlp"
Rejournal = 3600000000000
PriceLimit = 1
PriceBump = 10
AccountSlots = 16
GlobalSlots = 5120
AccountQueue = 64
GlobalQueue = 1024
Lifetime = 10800000000000

[Eth.GPO]
Blocks = 20
Percentile = 60
MaxHeaderHistory = 1024
MaxBlockHistory = 1024
MaxPrice = 500000000000
IgnorePrice = 2

[Node]
DataDir = "/home/worldland/gwangju"
IPCPath = "worldland.ipc"
HTTPHost = ""
HTTPPort = 8545
HTTPVirtualHosts = ["localhost"]
HTTPModules = ["net", "web3", "eth"]
AuthAddr = "localhost"
AuthPort = 8551
AuthVirtualHosts = ["localhost"]
WSHost = ""
WSPort = 8546
WSModules = ["net", "web3", "eth"]
GraphQLVirtualHosts = ["localhost"]

[Node.P2P]
MaxPeers = 50
NoDiscovery = false
BootstrapNodes = ["enode://4f4be8c67ac7b1fcfceb21a374a62c68f7f0528988f3b3d322bd6d94aeb745667f0c8e847881bbaeeba52eb1d346166301243222d5e22dd16ce70c57214178ca@43.200.52.189:30303", "enode://bbbf2734ce12b7aa258dd1e92e9cec7ea6b2ca6766f5741272c934904f3d182e08688aef3a368684c4c06b6adc2711c51e517bb9033824b2816c9d038c256cf9@3.36.252.183:30303", "enode://911771c7894782bced03377a13f1d8a4e8450d05e03eabab1d6daae70e1b91b6074c346d42ac4fae53d98d273efedd6cdd37d2f6715302de9736b29cc4aa7da2@13.250.246.202:30303"]
BootstrapNodesV5 = ["enr:-KG4QOtcP9X1FbIMOe17QNMKqDxCpm14jcX5tiOE4_TyMrFqbmhPZHK_ZPG2Gxb1GE2xdtodOfx9-cgvNtxnRyHEmC0ghGV0aDKQ9aX9QgAAAAD__________4JpZIJ2NIJpcIQDE8KdiXNlY3AyNTZrMaEDhpehBDbZjM_L9ek699Y7vhUJ-eAdMyQW_Fil522Y0fODdGNwgiMog3VkcIIjKA", "enr:-KG4QDyytgmE4f7AnvW-ZaUOIi9i79qX4JwjRAiXBZCU65wOfBu-3Nb5I7b_Rmg3KCOcZM_C3y5pg7EBU5XGrcLTduQEhGV0aDKQ9aX9QgAAAAD__________4JpZIJ2NIJpcIQ2_DUbiXNlY3AyNTZrMaEDKnz_-ps3UUOfHWVYaskI5kWYO_vtYMGYCQRAR3gHDouDdGNwgiMog3VkcIIjKA", "enr:-Ku4QImhMc1z8yCiNJ1TyUxdcfNucje3BGwEHzodEZUan8PherEo4sF7pPHPSIB1NNuSg5fZy7qFsjmUKs2ea1Whi0EBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpD1pf1CAAAAAP__________gmlkgnY0gmlwhBLf22SJc2VjcDI1NmsxoQOVphkDqal4QzPMksc5wnpuC3gvSC8AfbFOnZY_On34wIN1ZHCCIyg", "enr:-Ku4QP2xDnEtUXIjzJ_DhlCRN9SN99RYQPJL92TMlSv7U5C1YnYLjwOQHgZIUXw6c-BvRg2Yc2QsZxxoS_pPRVe0yK8Bh2F0dG5ldHOIAAAAAAAAAACEZXRoMpD1pf1CAAAAAP__________gmlkgnY0gmlwhBLf22SJc2VjcDI1NmsxoQMeFF5GrS7UZpAH2Ly84aLK-TyvH-dRo0JM1i8yygH50YN1ZHCCJxA", "enr:-Ku4QPp9z1W4tAO8Ber_NQierYaOStqhDqQdOPY3bB3jDgkjcbk6YrEnVYIiCBbTxuar3CzS528d2iE7TdJsrL-dEKoBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpD1pf1CAAAAAP__________gmlkgnY0gmlwhBLf22SJc2VjcDI1NmsxoQMw5fqqkw2hHC4F5HZZDPsNmPdB1Gi8JPQK7pRc9XHh-oN1ZHCCKvg", "enr:-IS4QLkKqDMy_ExrpOEWa59NiClemOnor-krjp4qoeZwIw2QduPC-q7Kz4u1IOWf3DDbdxqQIgC4fejavBOuUPy-HE4BgmlkgnY0gmlwhCLzAHqJc2VjcDI1NmsxoQLQSJfEAHZApkm5edTCZ_4qps_1k_ub2CxHFxi-gr2JMIN1ZHCCIyg", "enr:-IS4QDAyibHCzYZmIYZCjXwU9BqpotWmv2BsFlIq1V31BwDDMJPFEbox1ijT5c2Ou3kvieOKejxuaCqIcjxBjJ_3j_cBgmlkgnY0gmlwhAMaHiCJc2VjcDI1NmsxoQJIdpj_foZ02MXz4It8xKD7yUHTBx7lVFn3oeRP21KRV4N1ZHCCIyg", "enr:-Ku4QHqVeJ8PPICcWk1vSn_XcSkjOkNiTg6Fmii5j6vUQgvzMc9L1goFnLKgXqBJspJjIsB91LTOleFmyWWrFVATGngBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpC1MD8qAAAAAP__________gmlkgnY0gmlwhAMRHkWJc2VjcDI1NmsxoQKLVXFOhp2uX6jeT0DvvDpPcU8FWMjQdR4wMuORMhpX24N1ZHCCIyg", "enr:-Ku4QG-2_Md3sZIAUebGYT6g0SMskIml77l6yR-M_JXc-UdNHCmHQeOiMLbylPejyJsdAPsTHJyjJB2sYGDLe0dn8uYBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpC1MD8qAAAAAP__________gmlkgnY0gmlwhBLY-NyJc2VjcDI1NmsxoQORcM6e19T1T9gi7jxEZjk_sjVLGFscUNqAY9obgZaxbIN1ZHCCIyg", "enr:-Ku4QPn5eVhcoF1opaFEvg1b6JNFD2rqVkHQ8HApOKK61OIcIXD127bKWgAtbwI7pnxx6cDyk_nI88TrZKQaGMZj0q0Bh2F0dG5ldHOIAAAAAAAAAACEZXRoMpC1MD8qAAAAAP__________gmlkgnY0gmlwhDayLMaJc2VjcDI1NmsxoQK2sBOLGcUb4AwuYzFuAVCaNHA-dy24UuEKkeFNgCVCsIN1ZHCCIyg", "enr:-Ku4QEWzdnVtXc2Q0ZVigfCGggOVB2Vc1ZCPEc6j21NIFLODSJbvNaef1g4PxhPwl_3kax86YPheFUSLXPRs98vvYsoBh2F0dG5ldHOIAAAAAAAAAACEZXRoMpC1MD8qAAAAAP__________gmlkgnY0gmlwhDZBrP2Jc2VjcDI1NmsxoQM6jr8Rb1ktLEsVcKAPa08wCsKUmvoQ8khiOl_SLozf9IN1ZHCCIyg"]
StaticNodes = []
TrustedNodes = []
ListenAddr = ":30303"
DiscAddr = ""
EnableMsgEvents = false

[Node.HTTPTimeouts]
ReadTimeout = 30000000000
ReadHeaderTimeout = 30000000000
WriteTimeout = 30000000000
IdleTimeout = 120000000000

[Metrics]
HTTP = "127.0.0.1"
Port = 6060
InfluxDBEndpoint = "http://localhost:8086"
InfluxDBDatabase = "geth"
InfluxDBUsername = "test"
InfluxDBPassword = "test"
InfluxDBTags = "host=localhost"
InfluxDBToken = "test"
InfluxDBBucket = "geth"
InfluxDBOrganization = "geth"

```
````



### Command-line Options <a href="#command-line-options" id="command-line-options"></a>

A full list of command line help is listed below. You can always get the same information from your own **ETH-ECC** instance by running the following command:

```
./worldland -help
```

```
NAME:
   worldland - the ETH-ECC command line interface

USAGE:
   worldland [global options] command [command options] [arguments...]

COMMANDS:
   account                Manage accounts
   attach                 Start an interactive JavaScript environment (connect to node)
   console                Start an interactive JavaScript environment
   db                     Low level database operations
   dump                   Dump a specific block from storage
   dumpconfig             Show configuration values
   dumpgenesis            Dumps genesis block JSON configuration to stdout
   export                 Export blockchain into file
   export-preimages       Export the preimage database into an RLP stream
   import                 Import a blockchain file
   import-preimages       Import the preimage database from an RLP stream
   init                   Bootstrap and initialize a new genesis block
   js                     (DEPRECATED) Execute the specified JavaScript files
   license                Display license information
   makecache              Generate ethash verification cache (for testing)
   makedag                Generate ethash mining DAG (for testing)
   removedb               Remove blockchain and state databases
   show-deprecated-flags  Show flags that have been deprecated
   snapshot               A set of commands based on the snapshot
   version                Print version numbers
   version-check          Checks (online) for known Geth security vulnerabilities
   wallet                 Manage Ethereum presale wallets
   help, h                Shows a list of commands or help for one command

GLOBAL OPTIONS:
   
    --gwangju                      (default: false)
          Gwangju network: Error-Correction Codes Proof-of-Work Test Network
   
    --lve                          (default: false)
          LVE Network: Error-Correction Codes Proof-of-Work Main Network
   
    --seoul                        (default: false)
          Seoul Network: Error-Correction Codes Proof-of-Work Main Network
   
   ACCOUNT
   
    --allow-insecure-unlock        (default: false)
          Allow insecure account unlocking when account-related RPCs are exposed by http
   
    --keystore value              
          Directory for the keystore (default = inside the datadir)
   
    --lightkdf                     (default: false)
          Reduce key-derivation RAM & CPU usage at some expense of KDF strength
   
    --password value              
          Password file to use for non-interactive password input
   
    --pcscdpath value              (default: "/run/pcscd/pcscd.comm")
          Path to the smartcard daemon (pcscd) socket file
   
    --signer value                
          External signer (url or path to ipc file)
   
    --unlock value                
          Comma separated list of accounts to unlock
   
    --usb                          (default: false)
          Enable monitoring and management of USB hardware wallets
   
   ALIASED (deprecated)
   
    --miner.gastarget value        (default: 0)
          Target gas floor for mined blocks (deprecated)
   
    --nousb                        (default: false)
          Disables monitoring for and managing USB hardware wallets (deprecated)
   
    --whitelist value             
          Comma separated block number-to-hash mappings to enforce (<number>=<hash>)
          (deprecated in favor of --eth.requiredblocks)
   
   API AND CONSOLE
   
    --authrpc.addr value           (default: "localhost")
          Listening address for authenticated APIs
   
    --authrpc.jwtsecret value     
          Path to a JWT secret to use for authenticated RPC endpoints
   
    --authrpc.port value           (default: 8551)
          Listening port for authenticated APIs
   
    --authrpc.vhosts value         (default: "localhost")
          Comma separated list of virtual hostnames from which to accept requests (server
          enforced). Accepts '*' wildcard.
   
    --exec value                  
          Execute JavaScript statement
   
    --graphql                      (default: false)
          Enable GraphQL on the HTTP-RPC server. Note that GraphQL can only be started if
          an HTTP server is started as well.
   
    --graphql.corsdomain value    
          Comma separated list of domains from which to accept cross origin requests
          (browser enforced)
   
    --graphql.vhosts value         (default: "localhost")
          Comma separated list of virtual hostnames from which to accept requests (server
          enforced). Accepts '*' wildcard.
   
    --http                         (default: false)
          Enable the HTTP-RPC server
   
    --http.addr value              (default: "localhost")
          HTTP-RPC server listening interface
   
    --http.api value              
          API's offered over the HTTP-RPC interface
   
    --http.corsdomain value       
          Comma separated list of domains from which to accept cross origin requests
          (browser enforced)
   
    --http.port value              (default: 8545)
          HTTP-RPC server listening port
   
    --http.rpcprefix value        
          HTTP path path prefix on which JSON-RPC is served. Use '/' to serve on all
          paths.
   
    --http.vhosts value            (default: "localhost")
          Comma separated list of virtual hostnames from which to accept requests (server
          enforced). Accepts '*' wildcard.
   
    --ipcdisable                   (default: false)
          Disable the IPC-RPC server
   
    --ipcpath value               
          Filename for IPC socket/pipe within the datadir (explicit paths escape it)
   
    --jspath value                 (default: .)
          JavaScript root path for `loadScript`
   
    --preload value               
          Comma separated list of JavaScript files to preload into the console
   
    --rpc.allow-unprotected-txs    (default: false)
          Allow for unprotected (non EIP155 signed) transactions to be submitted via RPC
   
    --rpc.evmtimeout value         (default: 5s)
          Sets a timeout used for eth_call (0=infinite)
   
    --rpc.gascap value             (default: 50000000)
          Sets a cap on gas that can be used in eth_call/estimateGas (0=infinite)
   
    --rpc.txfeecap value           (default: 1)
          Sets a cap on transaction fee (in ether) that can be sent via the RPC APIs (0 =
          no cap)
   
    --ws                           (default: false)
          Enable the WS-RPC server
   
    --ws.addr value                (default: "localhost")
          WS-RPC server listening interface
   
    --ws.api value                
          API's offered over the WS-RPC interface
   
    --ws.origins value            
          Origins from which to accept websockets requests
   
    --ws.port value                (default: 8546)
          WS-RPC server listening port
   
    --ws.rpcprefix value          
          HTTP path prefix on which JSON-RPC is served. Use '/' to serve on all paths.
   
   DEVELOPER CHAIN
   
    --dev                          (default: false)
          Ephemeral proof-of-authority network with a pre-funded developer account, mining
          enabled
   
    --dev.gaslimit value           (default: 11500000)
          Initial block gas limit
   
    --dev.period value             (default: 0)
          Block period to use in developer mode (0 = mine only if transaction pending)
   
   ETHASH
   
    --ethash.cachedir value       
          Directory to store the ethash verification caches (default = inside the datadir)
   
    --ethash.cachesinmem value     (default: 2)
          Number of recent ethash caches to keep in memory (16MB each)
   
    --ethash.cacheslockmmap        (default: false)
          Lock memory maps of recent ethash caches
   
    --ethash.cachesondisk value    (default: 3)
          Number of recent ethash caches to keep on disk (16MB each)
   
    --ethash.dagdir value          (default: /home/infonet/.ethash)
          Directory to store the ethash mining DAGs
   
    --ethash.dagsinmem value       (default: 1)
          Number of recent ethash mining DAGs to keep in memory (1+GB each)
   
    --ethash.dagslockmmap          (default: false)
          Lock memory maps for recent ethash mining DAGs
   
    --ethash.dagsondisk value      (default: 2)
          Number of recent ethash mining DAGs to keep on disk (1+GB each)
   
   ETHEREUM
   
    --bloomfilter.size value       (default: 2048)
          Megabytes of memory allocated to bloom-filter for pruning
   
    --config value                
          TOML configuration file
   
    --datadir value                (default: /home/infonet/.ethereum)
          Data directory for the databases and keystore
   
    --datadir.ancient value       
          Root directory for ancient data (default = inside chaindata)
   
    --datadir.minfreedisk value   
          Minimum free disk space in MB, once reached triggers auto shut down (default =
          --cache.gc converted to MB, 0 = disabled)
   
    --eth.requiredblocks value    
          Comma separated block number-to-hash mappings to require for peering
          (<number>=<hash>)
   
    --exitwhensynced               (default: false)
          Exits after block synchronisation completes
   
    --gcmode value                 (default: "full")
          Blockchain garbage collection mode ("full", "archive")
   
    --networkid value              (default: 103)
          Explicitly set network id (integer)(For testnets: use --ropsten, --rinkeby,
          --goerli instead)
   
    --override.terminaltotaldifficulty value (default: 0)
          Manually specify TerminalTotalDifficulty, overriding the bundled setting
   
    --override.terminaltotaldifficultypassed (default: false)
          Manually specify TerminalTotalDifficultyPassed, overriding the bundled setting
   
    --snapshot                     (default: true)
          Enables snapshot-database mode (default = enable)
   
    --syncmode value               (default: snap)
          Blockchain sync mode ("snap", "full" or "light")
   
    --txlookuplimit value          (default: 2350000)
          Number of recent blocks to maintain transactions index for (default = about one
          year, 0 = entire chain)
   
   GAS PRICE ORACLE
   
    --gpo.blocks value             (default: 20)
          Number of recent blocks to check for gas prices
   
    --gpo.ignoreprice value        (default: 2)
          Gas price below which gpo will ignore transactions
   
    --gpo.maxprice value           (default: 500000000000)
          Maximum transaction priority fee (or gasprice before London fork) to be
          recommended by gpo
   
    --gpo.percentile value         (default: 60)
          Suggested gas price is the given percentile of a set of recent transaction gas
          prices
   
   LIGHT CLIENT
   
    --light.egress value           (default: 0)
          Outgoing bandwidth limit for serving light clients (kilobytes/sec, 0 =
          unlimited)
   
    --light.ingress value          (default: 0)
          Incoming bandwidth limit for serving light clients (kilobytes/sec, 0 =
          unlimited)
   
    --light.maxpeers value         (default: 100)
          Maximum number of light clients to serve, or light servers to attach to
   
    --light.nopruning              (default: false)
          Disable ancient light chain data pruning
   
    --light.nosyncserve            (default: false)
          Enables serving light clients before syncing
   
    --light.serve value            (default: 0)
          Maximum percentage of time allowed for serving LES requests (multi-threaded
          processing allows values over 100)
   
    --ulc.fraction value           (default: 75)
          Minimum % of trusted ultra-light servers required to announce a new head
   
    --ulc.onlyannounce             (default: false)
          Ultra light server sends announcements only
   
    --ulc.servers value           
          List of trusted ultra-light servers
   
   LOGGING AND DEBUGGING
   
    --fakepow                      (default: false)
          Disables proof-of-work verification
   
    --log.backtrace value         
          Request a stack trace at a specific logging statement (e.g. "block.go:271")
   
    --log.debug                    (default: false)
          Prepends log messages with call-site location (file and line number)
   
    --log.json                     (default: false)
          Format logs with JSON
   
    --nocompaction                 (default: false)
          Disables db compaction after import
   
    --pprof                        (default: false)
          Enable the pprof HTTP server
   
    --pprof.addr value             (default: "127.0.0.1")
          pprof HTTP server listening interface
   
    --pprof.blockprofilerate value (default: 0)
          Turn on block profiling with the given rate
   
    --pprof.cpuprofile value      
          Write CPU profile to the given file
   
    --pprof.memprofilerate value   (default: 524288)
          Turn on memory profiling with the given rate
   
    --pprof.port value             (default: 6060)
          pprof HTTP server listening port
   
    --remotedb value              
          URL for remote database
   
    --trace value                 
          Write execution trace to the given file
   
    --verbosity value              (default: 3)
          Logging verbosity: 0=silent, 1=error, 2=warn, 3=info, 4=debug, 5=detail
   
    --vmodule value               
          Per-module verbosity: comma-separated list of <pattern>=<level> (e.g.
          eth/*=5,p2p=4)
   
   METRICS AND STATS
   
    --ethstats value              
          Reporting URL of a ethstats service (nodename:secret@host:port)
   
    --metrics                      (default: false)
          Enable metrics collection and reporting
   
    --metrics.addr value           (default: "127.0.0.1")
          Enable stand-alone metrics HTTP server listening interface
   
    --metrics.expensive            (default: false)
          Enable expensive metrics collection and reporting
   
    --metrics.influxdb             (default: false)
          Enable metrics export/push to an external InfluxDB database
   
    --metrics.influxdb.bucket value (default: "geth")
          InfluxDB bucket name to push reported metrics to (v2 only)
   
    --metrics.influxdb.database value (default: "geth")
          InfluxDB database name to push reported metrics to
   
    --metrics.influxdb.endpoint value (default: "http://localhost:8086")
          InfluxDB API endpoint to report metrics to
   
    --metrics.influxdb.organization value (default: "geth")
          InfluxDB organization name (v2 only)
   
    --metrics.influxdb.password value (default: "test")
          Password to authorize access to the database
   
    --metrics.influxdb.tags value  (default: "host=localhost")
          Comma-separated InfluxDB tags (key/values) attached to all measurements
   
    --metrics.influxdb.token value (default: "test")
          Token to authorize access to the database (v2 only)
   
    --metrics.influxdb.username value (default: "test")
          Username to authorize access to the database
   
    --metrics.influxdbv2           (default: false)
          Enable metrics export/push to an external InfluxDB v2 database
   
    --metrics.port value           (default: 6060)
          Metrics HTTP server listening port
   
   MINER
   
    --mine                         (default: false)
          Enable mining
   
    --miner.etherbase value        (default: "0")
          Public address for block mining rewards (default = first account)
   
    --miner.extradata value       
          Block extra data set by the miner (default = client version)
   
    --miner.gaslimit value         (default: 30000000)
          Target gas ceiling for mined blocks
   
    --miner.gasprice value         (default: 0)
          Minimum gas price for mining a transaction
   
    --miner.notify value          
          Comma separated HTTP URL list to notify of new work packages
   
    --miner.notify.full            (default: false)
          Notify with pending block headers instead of work packages
   
    --miner.noverify               (default: false)
          Disable remote sealing verification
   
    --miner.recommit value         (default: 3s)
          Time interval to recreate the block being mined
   
    --miner.threads value          (default: 0)
          Number of CPU threads to use for mining
   
   MISC
   
    --help, -h                     (default: false)
          show help
   
    --ignore-legacy-receipts       (default: false)
          Geth will start up even if there are legacy receipts in freezer
   
   NETWORKING
   
    --bootnodes value             
          Comma separated enode URLs for P2P discovery bootstrap
   
    --discovery.dns value         
          Sets DNS discovery entry points (use "" to disable DNS)
   
    --discovery.port value         (default: 30303)
          Use a custom UDP port for P2P discovery
   
    --identity value              
          Custom node name
   
    --maxpeers value               (default: 50)
          Maximum number of network peers (network disabled if set to 0)
   
    --maxpendpeers value           (default: 0)
          Maximum number of pending connection attempts (defaults used if set to 0)
   
    --nat value                    (default: "any")
          NAT port mapping mechanism (any|none|upnp|pmp|extip:<IP>)
   
    --netrestrict value           
          Restricts network communication to the given IP networks (CIDR masks)
   
    --nodekey value               
          P2P node key file
   
    --nodekeyhex value            
          P2P node key as hex (for testing)
   
    --nodiscover                   (default: false)
          Disables the peer discovery mechanism (manual peer addition)
   
    --port value                   (default: 30303)
          Network listening port
   
    --v5disc                       (default: false)
          Enables the experimental RLPx V5 (Topic Discovery) mechanism
   
   PERFORMANCE TUNING
   
    --cache value                  (default: 1024)
          Megabytes of memory allocated to internal caching (default = 4096 mainnet full
          node, 128 light mode)
   
    --cache.blocklogs value        (default: 32)
          Size (in number of blocks) of the log cache for filtering
   
    --cache.database value         (default: 50)
          Percentage of cache memory allowance to use for database io
   
    --cache.gc value               (default: 25)
          Percentage of cache memory allowance to use for trie pruning (default = 25% full
          mode, 0% archive mode)
   
    --cache.noprefetch             (default: false)
          Disable heuristic state prefetch during block import (less CPU and disk IO, more
          time waiting for data)
   
    --cache.preimages              (default: false)
          Enable recording the SHA3/keccak preimages of trie keys
   
    --cache.snapshot value         (default: 10)
          Percentage of cache memory allowance to use for snapshot caching (default = 10%
          full mode, 20% archive mode)
   
    --cache.trie value             (default: 15)
          Percentage of cache memory allowance to use for trie caching (default = 15% full
          mode, 30% archive mode)
   
    --cache.trie.journal value     (default: "triecache")
          Disk journal directory for trie cache to survive node restarts
   
    --cache.trie.rejournal value   (default: 1h0m0s)
          Time interval to regenerate the trie cache journal
   
    --fdlimit value                (default: 0)
          Raise the open file descriptor resource limit (default = system fd limit)
   
   TRANSACTION POOL
   
    --txpool.accountqueue value    (default: 64)
          Maximum number of non-executable transaction slots permitted per account
   
    --txpool.accountslots value    (default: 16)
          Minimum number of executable transaction slots guaranteed per account
   
    --txpool.globalqueue value     (default: 1024)
          Maximum number of non-executable transaction slots for all accounts
   
    --txpool.globalslots value     (default: 5120)
          Maximum number of executable transaction slots for all accounts
   
    --txpool.journal value         (default: "transactions.rlp")
          Disk journal for local transaction to survive node restarts
   
    --txpool.lifetime value        (default: 3h0m0s)
          Maximum amount of time non-executable transaction are queued
   
    --txpool.locals value         
          Comma separated accounts to treat as locals (no flush, priority inclusion)
   
    --txpool.nolocals              (default: false)
          Disables price exemptions for locally submitted transactions
   
    --txpool.pricebump value       (default: 10)
          Price bump percentage to replace an already existing transaction
   
    --txpool.pricelimit value      (default: 1)
          Minimum gas price limit to enforce for acceptance into the pool
   
    --txpool.rejournal value       (default: 1h0m0s)
          Time interval to regenerate the local transaction journal
   
   VIRTUAL MACHINE
    --vmdebug                      (default: false)
          Record information useful for VM and contract debugging
   

COPYRIGHT:
   Copyright 2023- The ETH-ECC and go-ethereum Authors
```
