# Debug

The debug API gives you access to several non-standard RPC methods, which will allow you to inspect, debug and set certain debugging flags during runtime.

#### debug\_accountRange <a href="#debugaccountrange" id="debugaccountrange"></a>

Enumerates all accounts at a given block with paging capability. maxResults are returned in the page and the items have keys that come after the start key (hashed address).

If incompletes is false, then accounts for which the key preimage (i.e: the address) doesn't exist in db are skipped. NB: geth by default does not store preimages.

| CLIENT  | METHOD INVOCATION                                                                                                |
| ------- | ---------------------------------------------------------------------------------------------------------------- |
| Console | debug.accountRange(blockNrOrHash, start, maxResults, nocode, nostorage, incompletes)                             |
| RPC     | {"method": "debug\_accountRange", "params": \[blockNrOrHash, start, maxResults, nocode, nostorage, incompletes]} |

#### debug\_backtraceAt <a href="#debugbacktraceat" id="debugbacktraceat"></a>

Sets the logging backtrace location. When a backtrace location is set and a log message is emitted at that location, the stack of the goroutine executing the log statement will be printed to stderr.

The location is specified as \<filename>:\<line>.

| CLIENT  | METHOD INVOCATION                                     |
| ------- | ----------------------------------------------------- |
| Console | debug.backtraceAt(string)                             |
| RPC     | {"method": "debug\_backtraceAt", "params": \[string]} |

Example:

```javascript
> debug.backtraceAt("server.go:443")
```

#### debug\_blockProfile <a href="#debugblockprofile" id="debugblockprofile"></a>

Turns on block profiling for the given duration and writes profile data to disk. It uses a profile rate of 1 for most accurate information. If a different rate is desired, set the rate and write the profile manually using debug\_writeBlockProfile.

| CLIENT  | METHOD INVOCATION                                              |
| ------- | -------------------------------------------------------------- |
| Console | debug.blockProfile(file, seconds)                              |
| RPC     | {"method": "debug\_blockProfile", "params": \[string, number]} |

#### debug\_chaindbCompact <a href="#debugchaindbcompact" id="debugchaindbcompact"></a>

Flattens the entire key-value database into a single level, removing all unused slots and merging all keys.

| CLIENT  | METHOD INVOCATION                                  |
| ------- | -------------------------------------------------- |
| Console | debug.chaindbCompact()                             |
| RPC     | {"method": "debug\_chaindbCompact", "params": \[]} |

#### debug\_chaindbProperty <a href="#debugchaindbproperty" id="debugchaindbproperty"></a>

Returns leveldb properties of the key-value database.

| CLIENT  | METHOD INVOCATION                                           |
| ------- | ----------------------------------------------------------- |
| Console | debug.chaindbProperty(property string)                      |
| RPC     | {"method": "debug\_chaindbProperty", "params": \[property]} |

#### debug\_cpuProfile <a href="#debugcpuprofile" id="debugcpuprofile"></a>

Turns on CPU profiling for the given duration and writes profile data to disk.

| CLIENT  | METHOD INVOCATION                                            |
| ------- | ------------------------------------------------------------ |
| Console | debug.cpuProfile(file, seconds)                              |
| RPC     | {"method": "debug\_cpuProfile", "params": \[string, number]} |

#### debug\_dbAncient <a href="#debugdbancient" id="debugdbancient"></a>

Retrieves an ancient binary blob from the freezer. The freezer is a collection of append-only immutable files. The first argument kind specifies which table to look up data from. The list of all table kinds are as follows:

* headers: block headers
* hashes: canonical hash table (block number -> block hash)
* bodies: block bodies
* receipts: block receipts
* diffs: total difficulty table (block number -> td)

| CLIENT  | METHOD INVOCATION                                           |
| ------- | ----------------------------------------------------------- |
| Console | debug.dbAncient(kind string, number uint64)                 |
| RPC     | {"method": "debug\_dbAncient", "params": \[string, number]} |

#### debug\_dbAncients <a href="#debugdbancients" id="debugdbancients"></a>

Returns the number of ancient items in the ancient store.

| CLIENT  | METHOD INVOCATION               |
| ------- | ------------------------------- |
| Console | debug.dbAncients()              |
| RPC     | {"method": "debug\_dbAncients"} |

#### debug\_dbGet <a href="#debugdbget" id="debugdbget"></a>

Returns the raw value of a key stored in the database.

| CLIENT  | METHOD INVOCATION                            |
| ------- | -------------------------------------------- |
| Console | debug.dbGet(key string)                      |
| RPC     | {"method": "debug\_dbGet", "params": \[key]} |

#### debug\_dumpBlock <a href="#debugdumpblock" id="debugdumpblock"></a>

Retrieves the state that corresponds to the block number and returns a list of accounts (including storage and code).

| CLIENT  | METHOD INVOCATION                                   |
| ------- | --------------------------------------------------- |
| Go      | debug.DumpBlock(number uint64) (state.World, error) |
| Console | debug.traceBlockByHash(number, \[options])          |
| RPC     | {"method": "debug\_dumpBlock", "params": \[number]} |

**Example**

```javascript
> debug.dumpBlock(10)
{
    fff7ac99c8e4feb60c9750054bdc14ce1857f181: {
      balance: "49358640978154672",
      code: "",
      codeHash: "c5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
      nonce: 2,
      root: "56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
      storage: {}
    },
    fffbca3a38c3c5fcb3adbb8e63c04c3e629aafce: {
      balance: "3460945928",
      code: "",
      codeHash: "c5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
      nonce: 657,
      root: "56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
      storage: {}
    }
  },
  root: "19f4ed94e188dd9c7eb04226bd240fa6b449401a6c656d6d2816a87ccaf206f1"
}
```

#### debug\_freeOSMemory <a href="#debugfreeosmemory" id="debugfreeosmemory"></a>

Forces garbage collection

| CLIENT  | METHOD INVOCATION                                |
| ------- | ------------------------------------------------ |
| Go      | debug.FreeOSMemory()                             |
| Console | debug.freeOSMemory()                             |
| RPC     | {"method": "debug\_freeOSMemory", "params": \[]} |

#### debug\_freezeClient <a href="#debugfreezeclient" id="debugfreezeclient"></a>

Forces a temporary client freeze, normally when the server is overloaded. Available as part of LES light server.

| CLIENT  | METHOD INVOCATION                                    |
| ------- | ---------------------------------------------------- |
| Console | debug.freezeClient(node string)                      |
| RPC     | {"method": "debug\_freezeClient", "params": \[node]} |

#### debug\_gcStats <a href="#debuggcstats" id="debuggcstats"></a>

Returns garbage collection statistics.

See [https://golang.org/pkg/runtime/debug/#GCStats](https://golang.org/pkg/runtime/debug/#GCStats) for information about the fields of the returned object.

| CLIENT  | METHOD INVOCATION                           |
| ------- | ------------------------------------------- |
| Console | debug.gcStats()                             |
| RPC     | {"method": "debug\_gcStats", "params": \[]} |

#### debug\_getAccessibleState <a href="#debuggetaccessiblestate" id="debuggetaccessiblestate"></a>

Returns the first number where the node has accessible state on disk. This is the post-state of that block and the pre-state of the next block. The (from, to) parameters are the sequence of blocks to search, which can go either forwards or backwards.

Note: to get the last state pass in the range of blocks in reverse, i.e. (last, first).

| CLIENT  | METHOD INVOCATION                                              |
| ------- | -------------------------------------------------------------- |
| Console | debug.getAccessibleState(from, to rpc.BlockNumber)             |
| RPC     | {"method": "debug\_getAccessibleState", "params": \[from, to]} |

#### debug\_getBadBlocks <a href="#debuggetbadblocks" id="debuggetbadblocks"></a>

Returns a list of the last 'bad blocks' that the client has seen on the network and returns them as a JSON list of block-hashes.

| CLIENT  | METHOD INVOCATION                                |
| ------- | ------------------------------------------------ |
| Console | debug.getBadBlocks()                             |
| RPC     | {"method": "debug\_getBadBlocks", "params": \[]} |

#### debug\_getRawBlock <a href="#debuggetrawblock" id="debuggetrawblock"></a>

Retrieves and returns the RLP encoded block by number.

| CLIENT  | METHOD INVOCATION                                            |
| ------- | ------------------------------------------------------------ |
| Go      | debug.getRawBlock(blockNrOrHash) (string, error)             |
| Console | debug.getBlockRlp(blockNrOrHash)                             |
| RPC     | {"method": "debug\_getRawBlock", "params": \[blockNrOrHash]} |

References: [RLP](https://ethereum.org/en/developers/docs/data-structures-and-encoding/rlp/)

#### debug\_getRawHeader <a href="#debuggetrawheader" id="debuggetrawheader"></a>

Returns an RLP-encoded header.

| CLIENT  | METHOD INVOCATION                                             |
| ------- | ------------------------------------------------------------- |
| Console | debug.getRawHeader(blockNrOrHash)                             |
| RPC     | {"method": "debug\_getRawHeader", "params": \[blockNrOrHash]} |

#### debug\_getRawTransaction <a href="#debuggetrawtransaction" id="debuggetrawtransaction"></a>

Returns the bytes of the transaction.

| CLIENT  | METHOD INVOCATION                                                    |
| ------- | -------------------------------------------------------------------- |
| Console | debug.getRawTransaction(blockNrOrHash)                               |
| RPC     | {"method": "debug\_getRawTransaction", "params": \[transactionHash]} |

#### debug\_getModifiedAccountsByHash <a href="#debuggetmodifiedaccountsbyhash" id="debuggetmodifiedaccountsbyhash"></a>

Returns all accounts that have changed between the two blocks specified. A change is defined as a difference in nonce, balance, code hash, or storage hash. With one parameter, returns the list of accounts modified in the specified block.

| CLIENT  | METHOD INVOCATION                                                               |
| ------- | ------------------------------------------------------------------------------- |
| Console | debug.getModifiedAccountsByHash(startHash, endHash)                             |
| RPC     | {"method": "debug\_getModifiedAccountsByHash", "params": \[startHash, endHash]} |

#### debug\_getModifiedAccountsByNumber <a href="#debuggetmodifiedaccountsbynumber" id="debuggetmodifiedaccountsbynumber"></a>

Returns all accounts that have changed between the two blocks specified. A change is defined as a difference in nonce, balance, code hash or storage hash.

| CLIENT  | METHOD INVOCATION                                                               |
| ------- | ------------------------------------------------------------------------------- |
| Console | debug.getModifiedAccountsByNumber(startNum uint64, endNum uint64)               |
| RPC     | {"method": "debug\_getModifiedAccountsByNumber", "params": \[startNum, endNum]} |

**Note**

Geth only keeps recent trie nodes and preimages of keys in memory - for older blocks this information is deleted by Geth's garbage collection. This means that calls to debug\_GetModifiedAccountsByNumber on blocks that are old enough to be eligible for garbage collection will return an error due to the trie nodes and preimages being unavailable. To fix this, run Geth with --cache.preimages=true to prevent the relevant data being lost to the garbage collector

#### debug\_getRawReceipts <a href="#debuggetrawreceipts" id="debuggetrawreceipts"></a>

Returns the consensus-encoding of all receipts in a single block.

| CLIENT  | METHOD INVOCATION                                               |
| ------- | --------------------------------------------------------------- |
| Console | debug.getRawReceipts(blockNrOrHash)                             |
| RPC     | {"method": "debug\_getRawReceipts", "params": \[blockNrOrHash]} |

#### debug\_goTrace <a href="#debuggotrace" id="debuggotrace"></a>

Turns on Go runtime tracing for the given duration and writes trace data to disk.

| CLIENT  | METHOD INVOCATION                                         |
| ------- | --------------------------------------------------------- |
| Console | debug.goTrace(file, seconds)                              |
| RPC     | {"method": "debug\_goTrace", "params": \[string, number]} |

#### debug\_intermediateRoots <a href="#debugintermediateroots" id="debugintermediateroots"></a>

Executes a block (bad- or canon- or side-), and returns a list of intermediate roots: the stateroot after each transaction.

| CLIENT  | METHOD INVOCATION                                                  |
| ------- | ------------------------------------------------------------------ |
| Console | debug.intermediateRoots(blockHash, \[options])                     |
| RPC     | {"method": "debug\_intermediateRoots", "params": \[blockHash, {}]} |

#### debug\_memStats <a href="#debugmemstats" id="debugmemstats"></a>

Returns detailed runtime memory statistics.

See [https://golang.org/pkg/runtime/#MemStats](https://golang.org/pkg/runtime/#MemStats) for information about the fields of the returned object.

| CLIENT  | METHOD INVOCATION                            |
| ------- | -------------------------------------------- |
| Console | debug.memStats()                             |
| RPC     | {"method": "debug\_memStats", "params": \[]} |

#### debug\_mutexProfile <a href="#debugmutexprofile" id="debugmutexprofile"></a>

Turns on mutex profiling for nsec seconds and writes profile data to file. It uses a profile rate of 1 for most accurate information. If a different rate is desired, set the rate and write the profile manually.

| CLIENT  | METHOD INVOCATION                                          |
| ------- | ---------------------------------------------------------- |
| Console | debug.mutexProfile(file, nsec)                             |
| RPC     | {"method": "debug\_mutexProfile", "params": \[file, nsec]} |

#### debug\_preimage <a href="#debugpreimage" id="debugpreimage"></a>

Returns the preimage for a sha3 hash, if known.

| CLIENT  | METHOD INVOCATION                                |
| ------- | ------------------------------------------------ |
| Console | debug.preimage(hash)                             |
| RPC     | {"method": "debug\_preimage", "params": \[hash]} |

#### debug\_printBlock <a href="#debugprintblock" id="debugprintblock"></a>

Retrieves a block and returns its pretty printed form.

| CLIENT  | METHOD INVOCATION                                    |
| ------- | ---------------------------------------------------- |
| Console | debug.printBlock(number uint64)                      |
| RPC     | {"method": "debug\_printBlock", "params": \[number]} |

#### debug\_seedHash <a href="#debugseedhash" id="debugseedhash"></a>

Fetches and retrieves the seed hash of the block by number

| CLIENT  | METHOD INVOCATION                                  |
| ------- | -------------------------------------------------- |
| Go      | debug.SeedHash(number uint64) (string, error)      |
| Console | debug.seedHash(number, \[options])                 |
| RPC     | {"method": "debug\_seedHash", "params": \[number]} |

#### debug\_setBlockProfileRate <a href="#debugsetblockprofilerate" id="debugsetblockprofilerate"></a>

Sets the rate (in samples/sec) of goroutine block profile data collection. A non-zero rate enables block profiling, setting it to zero stops the profile. Collected profile data can be written using debug\_writeBlockProfile.

| CLIENT  | METHOD INVOCATION                                             |
| ------- | ------------------------------------------------------------- |
| Console | debug.setBlockProfileRate(rate)                               |
| RPC     | {"method": "debug\_setBlockProfileRate", "params": \[number]} |

#### debug\_setGCPercent <a href="#debugsetgcpercent" id="debugsetgcpercent"></a>

Sets the garbage collection target percentage. A negative value disables garbage collection.

| CLIENT  | METHOD INVOCATION                                 |
| ------- | ------------------------------------------------- |
| Go      | debug.SetGCPercent(v int)                         |
| Console | debug.setGCPercent(v)                             |
| RPC     | {"method": "debug\_setGCPercent", "params": \[v]} |

#### debug\_setHead <a href="#debugsethead" id="debugsethead"></a>

Sets the current head of the local chain by block number. **Note**, this is a destructive action and may severely damage your chain. Use with _extreme_ caution.

| CLIENT  | METHOD INVOCATION                                 |
| ------- | ------------------------------------------------- |
| Go      | debug.SetHead(number uint64)                      |
| Console | debug.setHead(number)                             |
| RPC     | {"method": "debug\_setHead", "params": \[number]} |

References: [Ethash](https://ethereum.org/en/developers/docs/consensus-mechanisms/pow/mining-algorithms/ethash/)

#### debug\_setMutexProfileFraction <a href="#debugsetmutexprofilefraction" id="debugsetmutexprofilefraction"></a>

Sets the rate of mutex profiling.

| CLIENT  | METHOD INVOCATION                                               |
| ------- | --------------------------------------------------------------- |
| Console | debug.setMutexProfileFraction(rate int)                         |
| RPC     | {"method": "debug\_setMutexProfileFraction", "params": \[rate]} |

#### debug\_setTrieFlushInterval <a href="#debugsettrieflushinterval" id="debugsettrieflushinterval"></a>

Configures how often in-memory state tries are persisted to disk. The interval needs to be in a format parsable by a [time.Duration](https://pkg.go.dev/time#ParseDuration). Note that the interval is not wall-clock time. Rather it is accumulated block processing time after which the state should be flushed. For example the value 0s will essentially turn on archive mode. If set to 1h, it means that after one hour of effective block processing time, the trie would be flushed. If one block takes 200ms, a flush would occur every 5\*3600=18000 blocks. The default interval for mainnet is 1h.

**Note:** this configuration will not be presisted through restarts.

| CLIENT  | METHOD INVOCATION                                                |
| ------- | ---------------------------------------------------------------- |
| Console | debug.setTrieFlushInterval(interval string)                      |
| RPC     | {"method": "debug\_setTrieFlushInterval", "params": \[interval]} |

#### debug\_stacks <a href="#debugstacks" id="debugstacks"></a>

Returns a printed representation of the stacks of all goroutines. Note that the web3 wrapper for this method takes care of the printing and does not return the string.

| CLIENT  | METHOD INVOCATION                          |
| ------- | ------------------------------------------ |
| Console | debug.stacks()                             |
| RPC     | {"method": "debug\_stacks", "params": \[]} |

#### debug\_standardTraceBlockToFile <a href="#debugstandardtraceblocktofile" id="debugstandardtraceblocktofile"></a>

When JS-based tracing (see below) was first implemented, the intended usecase was to enable long-running tracers that could stream results back via a subscription channel. This method works a bit differently. (For full details, see [PR](https://github.com/ethereum/go-ethereum/pull/17914))

* It streams output to disk during the execution, to not blow up the memory usage on the node
* It uses jsonl as output format (to allow streaming)
* Uses a cross-client standardized output, so called 'standard json'
  * Uses op for string-representation of opcode, instead of op/opName for numeric/string, and other simlar small differences.
  * has refund
  * Represents memory as a contiguous chunk of data, as opposed to a list of 32-byte segments like debug\_traceTransaction

This means that this method is only 'useful' for callers who control the node -- at least sufficiently to be able to read the artefacts from the filesystem after the fact.

The method can be used to dump a certain transaction out of a given block:

```javascript
> debug.standardTraceBlockToFile("0x0bbe9f1484668a2bf159c63f0cf556ed8c8282f99e3ffdb03ad2175a863bca63", {txHash:"0x4049f61ffbb0747bb88dc1c85dd6686ebf225a3c10c282c45a8e0c644739f7e9", disableMemory:true})
["/tmp/block_0x0bbe9f14-14-0x4049f61f-099048234"]
```

Or all txs from a block:

```javascript
> debug.standardTraceBlockToFile("0x0bbe9f1484668a2bf159c63f0cf556ed8c8282f99e3ffdb03ad2175a863bca63", {disableMemory:true})
["/tmp/block_0x0bbe9f14-0-0xb4502ea7-409046657", "/tmp/block_0x0bbe9f14-1-0xe839be8f-954614764", "/tmp/block_0x0bbe9f14-2-0xc6e2052f-542255195", "/tmp/block_0x0bbe9f14-3-0x01b7f3fe-209673214", "/tmp/block_0x0bbe9f14-4-0x0f290422-320999749", "/tmp/block_0x0bbe9f14-5-0x2dc0fb80-844117472", "/tmp/block_0x0bbe9f14-6-0x35542da1-256306111", "/tmp/block_0x0bbe9f14-7-0x3e199a08-086370834", "/tmp/block_0x0bbe9f14-8-0x87778b88-194603593", "/tmp/block_0x0bbe9f14-9-0xbcb081ba-629580052", "/tmp/block_0x0bbe9f14-10-0xc254381a-578605923", "/tmp/block_0x0bbe9f14-11-0xcc434d58-405931366", "/tmp/block_0x0bbe9f14-12-0xce61967d-874423181", "/tmp/block_0x0bbe9f14-13-0x05a20b35-267153288", "/tmp/block_0x0bbe9f14-14-0x4049f61f-606653767", "/tmp/block_0x0bbe9f14-15-0x46d473d2-614457338", "/tmp/block_0x0bbe9f14-16-0x35cf5500-411906321", "/tmp/block_0x0bbe9f14-17-0x79222961-278569788", "/tmp/block_0x0bbe9f14-18-0xad84e7b1-095032683", "/tmp/block_0x0bbe9f14-19-0x4bd48260-019097038", "/tmp/block_0x0bbe9f14-20-0x1517411d-292624085", "/tmp/block_0x0bbe9f14-21-0x6857e350-971385904", "/tmp/block_0x0bbe9f14-22-0xbe3ae2ca-236639695"]

```

Files are created in a temp-location, with the naming standard block\_\<blockhash:4>-\<txindex>-\<txhash:4>-\<random suffix>. Each opcode immediately streams to file, with no in-geth buffering aside from whatever buffering the os normally does.

On the server side, it also adds some more info when regenerating historical state, namely, the reexec-number if required historical state is not avaiable is encountered, so a user can experiment with increasing that setting. It also prints out the remaining block until it reaches target:

`INFO [10-15|13:48:25.263] Regenerating historical state block=2385959 target=2386012 remaining=53 elapsed=3m30.990537767s INFO [10-15|13:48:33.342] Regenerating historical state block=2386012 target=2386012 remaining=0 elapsed=3m39.070073163s INFO [10-15|13:48:33.343] Historical state regenerated block=2386012 elapsed=3m39.070454362s nodes=10.03mB preimages=652.08kB INFO [10-15|13:48:33.352] Wrote trace file=/tmp/block_0x14490c57-0-0xfbbd6d91-715824834 INFO [10-15|13:48:33.352] Wrote trace file=/tmp/block_0x14490c57-1-0x71076194-187462969 INFO [10-15|13:48:34.421] Wrote trace file=/tmp/block_0x14490c57-2-0x3f4263fe-056924484`

The options is as follows:

```javascript
type StdTraceConfig struct {
  *vm.LogConfig
  Reexec *uint64
  TxHash *common.Hash
}
```

#### debug\_standardTraceBadBlockToFile <a href="#debugstandardtracebadblocktofile" id="debugstandardtracebadblocktofile"></a>

This method is similar to debug\_standardTraceBlockToFile, but can be used to obtain info about a block which has been _rejected_ as invalid (for some reason).

#### debug\_startCPUProfile <a href="#debugstartcpuprofile" id="debugstartcpuprofile"></a>

Turns on CPU profiling indefinitely, writing to the given file.

| CLIENT  | METHOD INVOCATION                                         |
| ------- | --------------------------------------------------------- |
| Console | debug.startCPUProfile(file)                               |
| RPC     | {"method": "debug\_startCPUProfile", "params": \[string]} |

#### debug\_startGoTrace <a href="#debugstartgotrace" id="debugstartgotrace"></a>

Starts writing a Go runtime trace to the given file.

| CLIENT  | METHOD INVOCATION                                      |
| ------- | ------------------------------------------------------ |
| Console | debug.startGoTrace(file)                               |
| RPC     | {"method": "debug\_startGoTrace", "params": \[string]} |

#### debug\_stopCPUProfile <a href="#debugstopcpuprofile" id="debugstopcpuprofile"></a>

Stops an ongoing CPU profile.

| CLIENT  | METHOD INVOCATION                                  |
| ------- | -------------------------------------------------- |
| Console | debug.stopCPUProfile()                             |
| RPC     | {"method": "debug\_stopCPUProfile", "params": \[]} |

#### debug\_stopGoTrace <a href="#debugstopgotrace" id="debugstopgotrace"></a>

Stops writing the Go runtime trace.

| CLIENT  | METHOD INVOCATION                               |
| ------- | ----------------------------------------------- |
| Console | debug.startGoTrace(file)                        |
| RPC     | {"method": "debug\_stopGoTrace", "params": \[]} |

#### debug\_storageRangeAt <a href="#debugstoragerangeat" id="debugstoragerangeat"></a>

Returns the storage at the given block height and transaction index. The result can be paged by providing a maxResult to cap the number of storage slots returned as well as specifying the offset via keyStart (hash of storage key).

| CLIENT  | METHOD INVOCATION                                                                                        |
| ------- | -------------------------------------------------------------------------------------------------------- |
| Console | debug.storageRangeAt(blockHash, txIdx, contractAddress, keyStart, maxResult)                             |
| RPC     | {"method": "debug\_storageRangeAt", "params": \[blockHash, txIdx, contractAddress, keyStart, maxResult]} |

#### debug\_traceBadBlock <a href="#debugtracebadblock" id="debugtracebadblock"></a>

Returns the structured logs created during the execution of EVM against a block pulled from the pool of bad ones and returns them as a JSON object. For the second parameter see [TraceConfig](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#traceconfig) reference.

| CLIENT  | METHOD INVOCATION                                              |
| ------- | -------------------------------------------------------------- |
| Console | debug.traceBadBlock(blockHash, \[options])                     |
| RPC     | {"method": "debug\_traceBadBlock", "params": \[blockHash, {}]} |

#### debug\_traceBlock <a href="#debugtraceblock" id="debugtraceblock"></a>

The traceBlock method will return a full stack trace of all invoked opcodes of all transaction that were included in this block. **Note**, the parent of this block must be present or it will fail. For the second parameter see [TraceConfig](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#traceconfig) reference.

| CLIENT  | METHOD INVOCATION                                                         |
| ------- | ------------------------------------------------------------------------- |
| Go      | debug.TraceBlock(blockRlp \[]byte, config \*TraceConfig) BlockTraceResult |
| Console | debug.traceBlock(tblockRlp, \[options])                                   |
| RPC     | {"method": "debug\_traceBlock", "params": \[blockRlp, {}]}                |

References: [RLP](https://ethereum.org/en/developers/docs/data-structures-and-encoding/rlp/)

**Example**

```javascript
> debug.traceBlock("0xblock_rlp")
{
  gas: 85301,
  returnValue: "",
  structLogs: [{
      depth: 1,
      error: "",
      gas: 162106,
      gasCost: 3,
      memory: null,
      op: "PUSH1",
      pc: 0,
      stack: [],
      storage: {}
  },
    /* snip */
  {
      depth: 1,
      error: "",
      gas: 100000,
      gasCost: 0,
      memory: ["0000000000000000000000000000000000000000000000000000000000000006", "0000000000000000000000000000000000000000000000000000000000000000", "0000000000000000000000000000000000000000000000000000000000000060"],
      op: "STOP",
      pc: 120,
      stack: ["00000000000000000000000000000000000000000000000000000000d67cbec9"],
      storage: {
        0000000000000000000000000000000000000000000000000000000000000004: "8241fa522772837f0d05511f20caa6da1d5a3209000000000000000400000001",
        0000000000000000000000000000000000000000000000000000000000000006: "0000000000000000000000000000000000000000000000000000000000000001",
        f652222313e28459528d920b65115c16c04f3efc82aaedc97be59f3f377c0d3f: "00000000000000000000000002e816afc1b5c0f39852131959d946eb3b07b5ad"
      }
  }]
```

#### debug\_traceBlockByNumber <a href="#debugtraceblockbynumber" id="debugtraceblockbynumber"></a>

Similar to [debug\_traceBlock](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#debug\_traceblock), traceBlockByNumber accepts a block number and will replay the block that is already present in the database. For the second parameter see [TraceConfig](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#traceconfig) reference.

| CLIENT  | METHOD INVOCATION                                                              |
| ------- | ------------------------------------------------------------------------------ |
| Go      | debug.TraceBlockByNumber(number uint64, config \*TraceConfig) BlockTraceResult |
| Console | debug.traceBlockByNumber(number, \[options])                                   |
| RPC     | {"method": "debug\_traceBlockByNumber", "params": \[number, {}]}               |

References: [RLP](https://ethereum.org/en/developers/docs/data-structures-and-encoding/rlp/)

#### debug\_traceBlockByHash <a href="#debugtraceblockbyhash" id="debugtraceblockbyhash"></a>

Similar to [debug\_traceBlock](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#debug\_traceblock), traceBlockByHash accepts a block hash and will replay the block that is already present in the database. For the second parameter see [TraceConfig](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#traceconfig) reference.

| CLIENT  | METHOD INVOCATION                                                               |
| ------- | ------------------------------------------------------------------------------- |
| Go      | debug.TraceBlockByHash(hash common.Hash, config \*TraceConfig) BlockTraceResult |
| Console | debug.traceBlockByHash(hash, \[options])                                        |
| RPC     | {"method": "debug\_traceBlockByHash", "params": \[hash {}]}                     |

References: [RLP](https://ethereum.org/en/developers/docs/data-structures-and-encoding/rlp/)

#### debug\_traceBlockFromFile <a href="#debugtraceblockfromfile" id="debugtraceblockfromfile"></a>

Similar to [debug\_traceBlock](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#debug\_traceblock), traceBlockFromFile accepts a file containing the RLP of the block. For the second parameter see [TraceConfig](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#traceconfig) reference.

| CLIENT  | METHOD INVOCATION                                                                |
| ------- | -------------------------------------------------------------------------------- |
| Go      | debug.TraceBlockFromFile(fileName string, config \*TraceConfig) BlockTraceResult |
| Console | debug.traceBlockFromFile(fileName, \[options])                                   |
| RPC     | {"method": "debug\_traceBlockFromFile", "params": \[fileName, {}]}               |

References: [RLP](https://ethereum.org/en/developers/docs/data-structures-and-encoding/rlp/)

#### debug\_traceCall <a href="#debugtracecall" id="debugtracecall"></a>

The debug\_traceCall method lets you run an eth\_call within the context of the given block execution using the final state of parent block as the base. The first argument (just as in eth\_call) is a [transaction object](https://geth.ethereum.org/docs/interacting-with-geth/rpc/objects#transaction-call-object). The block can be specified either by hash or by number as the second argument. The trace can be configured similar to debug\_traceTransaction, see [TraceConfig](https://geth.ethereum.org/docs/interacting-with-geth/rpc/ns-debug#traceconfig). The method returns the same output as debug\_traceTransaction.

| CLIENT  | METHOD INVOCATION                                                                                                           |
| ------- | --------------------------------------------------------------------------------------------------------------------------- |
| Go      | debug.TraceCall(args ethapi.CallArgs, blockNrOrHash rpc.BlockNumberOrHash, config \*TraceConfig) (\*ExecutionResult, error) |
| Console | debug.traceCall(object, blockNrOrHash, \[options])                                                                          |
| RPC     | {"method": "debug\_traceCall", "params": \[object, blockNrOrHash, {}]}                                                      |

**Example**

No specific call options:

```javascript
> debug.traceCall(null, "0x0")
{
  failed: false,
  gas: 53000,
  returnValue: "",
  structLogs: []
}
```

Tracing a call with a destination and specific sender, disabling the storage and memory output (less data returned over RPC)

```javascript
debug.traceCall(
  {
    from: '0xdeadbeef29292929192939494959594933929292',
    to: '0xde929f939d939d393f939393f93939f393929023',
    gas: '0x7a120',
    data: '0xf00d4b5d00000000000000000000000001291230982139282304923482304912923823920000000000000000000000001293123098123928310239129839291010293810'
  },
  'latest',
  { disableStorage: true, disableMemory: true }
);
```

It is possible to supply 'overrides' for both state-data (accounts/storage) and block data (number, timestamp etc). In the example below, a call which executes NUMBER is performed, and the overridden number is placed on the stack:

```javascript
> debug.traceCall({
	from: eth.accounts[0],
	value:"0x1",
	gasPrice: "0xffffffff",
	gas: "0xffff",
	input: "0x43"},
	"latest",
	{"blockoverrides":
		{"number": "0x50"}
	})
{
  failed: false,
  gas: 53018,
  returnValue: "",
  structLogs: [{
      depth: 1,
      gas: 12519,
      gasCost: 2,
      op: "NUMBER",
      pc: 0,
      stack: []
  }, {
      depth: 1,
      gas: 12517,
      gasCost: 0,
      op: "STOP",
      pc: 1,
      stack: ["0x50"]
  }]
}
```

Curl example:

```sh
> curl -H "Content-Type: application/json" -X POST  localhost:8545 --data '{"jsonrpc":"2.0","method":"debug_traceCall","params":[null, "pending"],"id":1}'
{"jsonrpc":"2.0","id":1,"result":{"gas":53000,"failed":false,"returnValue":"","structLogs":[]}}
```

#### debug\_traceChain <a href="#debugtracechain" id="debugtracechain"></a>

Returns the structured logs created during the execution of EVM between two blocks (excluding start) as a JSON object. This endpoint must be invoked via debug\_subscribe as follows:

```javascript
const res = provider.send('debug_subscribe', ['traceChain', '0x3f3a2a', '0x3f3a2b'])`
```

please refer to the [subscription page](https://geth.ethereum.org/docs/interacting-with-geth/rpc/pubsub) for more details.

#### debug\_traceTransaction <a href="#debugtracetransaction" id="debugtracetransaction"></a>

**OBS** In most scenarios, debug.standardTraceBlockToFile is better suited for tracing!

The traceTransaction debugging method will attempt to run the transaction in the exact same manner as it was executed on the network. It will replay any transaction that may have been executed prior to this one before it will finally attempt to execute the transaction that corresponds to the given hash.

| CLIENT  | METHOD INVOCATION                                                                           |
| ------- | ------------------------------------------------------------------------------------------- |
| Go      | debug.TraceTransaction(txHash common.Hash, config \*TraceConfig) (\*ExecutionResult, error) |
| Console | debug.traceTransaction(txHash, \[options])                                                  |
| RPC     | {"method": "debug\_traceTransaction", "params": \[txHash, {}]}                              |

**TraceConfig**

In addition to the hash of the transaction you may give it a secondary _optional_ argument, which specifies the options for this specific call. The possible options are:

* disableStorage: BOOL. Setting this to true will disable storage capture (default = false).
* disableStack: BOOL. Setting this to true will disable stack capture (default = false).
* enableMemory: BOOL. Setting this to true will enable memory capture (default = false).
* enableReturnData: BOOL. Setting this to true will enable return data capture (default = false).
* tracer: STRING. Name for built-in tracer or Javascript expression. See below for more details.

If set, the previous four arguments will be ignored.

* timeout: STRING. Overrides the default timeout of 5 seconds for JavaScript-based tracing calls. Valid values are described [here](https://golang.org/pkg/time/#ParseDuration).
* tracerConfig: Config for the specified tracer. For example see callTracer's [config](https://geth.ethereum.org/docs/developers/evm-tracing/built-in-tracers#config).

Geth comes with a bundle of [built-in tracers](https://geth.ethereum.org/docs/developers/evm-tracing/built-in-tracers), each providing various data about a transaction. This method defaults to the [struct logger](https://geth.ethereum.org/docs/developers/evm-tracing/built-in-tracers#structopcode-logger). The tracer field of the second parameter can be set to use any of the other tracers. Alternatively a [custom tracer](https://geth.ethereum.org/docs/developers/evm-tracing/custom-tracer) can be implemented in either Go or Javascript.

**Example**

```javascript
> debug.traceTransaction("0x2059dd53ecac9827faad14d364f9e04b1d5fe5b506e3acc886eff7a6f88a696a")
{
  gas: 85301,
  returnValue: "",
  structLogs: [{
      depth: 1,
      error: "",
      gas: 162106,
      gasCost: 3,
      memory: null,
      op: "PUSH1",
      pc: 0,
      stack: [],
      storage: {}
  },
    /* snip */
  {
      depth: 1,
      error: "",
      gas: 100000,
      gasCost: 0,
      memory: ["0000000000000000000000000000000000000000000000000000000000000006", "0000000000000000000000000000000000000000000000000000000000000000", "0000000000000000000000000000000000000000000000000000000000000060"],
      op: "STOP",
      pc: 120,
      stack: ["00000000000000000000000000000000000000000000000000000000d67cbec9"],
      storage: {
        0000000000000000000000000000000000000000000000000000000000000004: "8241fa522772837f0d05511f20caa6da1d5a3209000000000000000400000001",
        0000000000000000000000000000000000000000000000000000000000000006: "0000000000000000000000000000000000000000000000000000000000000001",
        f652222313e28459528d920b65115c16c04f3efc82aaedc97be59f3f377c0d3f: "00000000000000000000000002e816afc1b5c0f39852131959d946eb3b07b5ad"
      }
  }]
```

#### debug\_verbosity <a href="#debugverbosity" id="debugverbosity"></a>

Sets the logging verbosity ceiling. Log messages with level up to and including the given level will be printed.

The verbosity of individual packages and source files can be raised using debug\_vmodule.

| CLIENT  | METHOD INVOCATION                                 |
| ------- | ------------------------------------------------- |
| Console | debug.verbosity(level)                            |
| RPC     | {"method": "debug\_vmodule", "params": \[number]} |

#### debug\_vmodule <a href="#debugvmodule" id="debugvmodule"></a>

Sets the logging verbosity pattern.

| CLIENT  | METHOD INVOCATION                                 |
| ------- | ------------------------------------------------- |
| Console | debug.vmodule(string)                             |
| RPC     | {"method": "debug\_vmodule", "params": \[string]} |

**Examples**

If you want to see messages from a particular Go package (directory) and all subdirectories, use:

```javascript
> debug.vmodule("eth/*=6")
```

If you want to restrict messages to a particular package (e.g. p2p) but exclude subdirectories, use:

```javascript
> debug.vmodule("p2p=6")
```

If you want to see log messages from a particular source file, use

```javascript
> debug.vmodule("server.go=6")
```

You can compose these basic patterns. If you want to see all output from peer.go in a package below eth (eth/peer.go, eth/downloader/peer.go) as well as output from package p2p at level <= 5, use:

```javascript
debug.vmodule('eth/*/peer.go=6,p2p=5');
```

#### debug\_writeBlockProfile <a href="#debugwriteblockprofile" id="debugwriteblockprofile"></a>

Writes a goroutine blocking profile to the given file.

| CLIENT  | METHOD INVOCATION                                           |
| ------- | ----------------------------------------------------------- |
| Console | debug.writeBlockProfile(file)                               |
| RPC     | {"method": "debug\_writeBlockProfile", "params": \[string]} |

#### debug\_writeMemProfile <a href="#debugwritememprofile" id="debugwritememprofile"></a>

Writes an allocation profile to the given file. Note that the profiling rate cannot be set through the API, it must be set on the command line using the --pprof.memprofilerate flag.

| CLIENT  | METHOD INVOCATION                                           |
| ------- | ----------------------------------------------------------- |
| Console | debug.writeMemProfile(file string)                          |
| RPC     | {"method": "debug\_writeBlockProfile", "params": \[string]} |

#### debug\_writeMutexProfile <a href="#debugwritemutexprofile" id="debugwritemutexprofile"></a>

Writes a goroutine blocking profile to the given file.

| CLIENT  | METHOD INVOCATION                                         |
| ------- | --------------------------------------------------------- |
| Console | debug.writeMutexProfile(file)                             |
| RPC     | {"method": "debug\_writeMutexProfile", "params": \[file]} |