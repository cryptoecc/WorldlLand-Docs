# Mining



The **WorldLand** blockchain is a proof-of-work blockchain. Nodes in **WorldLand** compete by running a specific algorithm called **ECCPoW**. The node that solved the algorithm the fastest creates and propagates the block. Other nodes verify that the received block actually solved the algorithm and accept the block only if it is verified. The series of processes that solve proof-of-work algorithms and generate blocks is called mining. ETH-ECC supports **CPU mining** of **ECCPoW** via the built-in miner.





ETH-ECC 노드가 시작되어도 기본적으로는 채굴을 하지 않습니다. 채굴을 위해서는 직접 설정이 필요합니다. -mine 옵션을 통해서 노드가광부로 시작하도록 할 수 있습니다.

```sh
$ ./worldland -mine
```



또한 JSON-RPC 콘솔의 miner 모듈을 사용하여 노드   실행중에 채굴을시작하고 중지할 수도 있습니다 .



miner.start() 명령을 통해서 채굴을 시작할 수 있습니다. 입력값으로 정수를 주면, 해당 수의 쓰레드로 마이닝이 실행됩니다.&#x20;

```
> miner.start(4)
INFO [08-04|15:05:45.206] Updated mining threads                   threads=4
```

miner.start() 명령은 노드의 채굴을 중지합니다.

```
> miner.stop()
null
```



네트워크의 동기화 되지 않고 채굴을 진행하면, 새로운 블록체인을 만들어 나가는 것과 같으므로 의미가 없습니다. 따라서 ETH-ECC 노드는 동기화가 완료될 때까지 채굴을 지연하고, 동기화과 완료된 후에 채굴이 자동으로 진행됩니다.

그런 다음 콘솔에서 동기화 진행률을 확인하려면 다음을 수행하십시오.

```sh
eth.syncing
```



동기화과 진행중인경우 다음과 같이 출력됩니다.

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



동기화가 false를 반환하면 동기화가 모두 완료된 것입니다.&#x20;

```
> eth.syncing
false
```



&#x20;채굴자로  기록될 etherbase 계정을 설정해야합니다.  etherbase 계정은 기본적으로 노드의   계정.집합인   eth.accounts 의 첫번째 계정으로 설정됩니다. 하지만  -miner.etherbase 명령을 사용하여 대체 주소로 설정할 수 있습니다.

<pre class="language-sh"><code class="lang-sh"><strong>$ ./worldland -miner.etherbase 'YOUR_ACCOUNT' -mine
</strong></code></pre>

사용 가능한 계정이 없으면 자동으로 계정이 생성되고 이더베이스로 설정됩니다.  콘솔의 마이너 모듈을 사용하여 수동으로 이더베이스를 변경할 수 있습니다. etherbase는 로컬 노드에 포함되어 있을 필요는 없으며, 기존의 계정이면 문제가 없습니다.&#x20;

```sh
miner.setEtherbase(eth.accounts[2])
```



채굴된 블록에 추가 데이터(32바이트)를 추가하여 데이터를 저장할 수 있습니다. 일반적으로 유니코드로 디코딩되므로, 콘솔의miner.setExtra() 명령어를 통해  원하는 데이터를 블록에 추가할 수 있습니다.

```sh
miner.setExtra("worldland")
```

콘솔을 사용하여 H/s(초당 해시 작업) 단위로 현재 해시 속도를 확인할 수도 있습니다.

```sh
eth.hashrate
 712000
```

eth,getBalance() 명령을 통해서 채굴을 통해 증가된 게정 잔액을 확인할 수 있습니다.

```sh
eth.getBalance(eth.coinbase).toNumber();
 '34698870000000'
```



잔액이   증가한  이후에  변동될 수 있습니다. 로컬 블록체인에서는 가장 먼저 생성된 블록이더라도, 아직 전파되지 않은 더 먼저 생성된 블록이 있어 재구성될 수 있습니다. 체인이 재구성되면, 생성한 블록이 포함되지 않고, 블록 보상이 적용되지 않습니다. 생성된 블록이 깊이가 깊어질 수록 안전해집니다. 로그에서는 무분별한 잔액 변동을 줄이기 위해 7개의 블록 깊이 이상의 채굴 블록만을 표시합니다.&#x20;

```
INFO [08-04|15:38:40.370] 🔗 block reached canonical chain          number=31720 hash=aaf485..dd2528
INFO [08-04|15:38:40.370] 🔨 mined potential block                  number=31727 hash=51968c..ba14fb
```



### &#x20;<a href="#summary" id="summary"></a>
