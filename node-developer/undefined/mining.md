# Mining



The **WorldLand** blockchain is a proof-of-work blockchain. Nodes in **WorldLand** compete by running a specific algorithm called **ECCPoW**. The node that solved the algorithm the fastest creates and propagates the block. Other nodes verify that the received block actually solved the algorithm and accept the block only if it is verified. The series of processes that solve proof-of-work algorithms and generate blocks is called mining. ETH-ECC supports **CPU mining** of **ECCPoW** via the built-in miner.



Geth가 시작되면 기본적으로 채굴되지 않습니다. 채굴을 특별히 지시하지 않는 한 채굴자가 아닌 노드로만 작동합니다. Geth는 --mine 플래그가 제공 되면 (CPU) 광부로 시작합니다 .

```sh
geth --mine
```

[콘솔을](https://geth.ethereum.org/docs/interacting-with-geth/javascript-console) 사용하여 런타임에 CPU 마이닝을 시작하고 중지할 수도 있습니다 .

```javascript
miner.start();
true;
miner.stop();
true;
```

채굴은 네트워크와 동기화된 경우에만 의미가 있습니다(합의 블록 위에서 채굴하기 때문에). 따라서 블록체인 다운로더/동기화 장치는 동기화가 완료될 때까지 채굴을 지연하고, 그 후에 miner.stop() 으로 취소하지 않는 한 채굴이 자동으로 시작됩니다 .

GPU 마이닝과 마찬가지로 etherbase 계정을 설정해야 합니다. 이는 기본적으로 키 저장소의 기본 계정이지만 --miner.etherbase 명령을 사용하여 대체 주소로 설정할 수 있습니다.

```sh
geth --miner.etherbase '0xC95767AC46EA2A9162F0734651d6cF17e5BfcF10' --mine
```

사용 가능한 계정이 없으면 계정이 생성되고 자동으로 코인베이스로 구성됩니다. Javascript 콘솔을 사용하여 런타임에 etherbase 계정을 재설정할 수 있습니다.

```sh
miner.setEtherbase(eth.accounts[2])
```

etherbase는 로컬 계정의 주소일 필요는 없으며 기존 계정으로 설정하기만 하면 됩니다.

채굴된 블록에 추가 데이터(32바이트만)를 추가하는 옵션이 있습니다. 관례적으로 이것은 유니코드 문자열로 해석되므로 Javascript 콘솔에서 miner.setExtra를 사용하여 짧은 베니티 태그를 추가하는 데 사용할 수 있습니다 .

```sh
miner.setExtra("ΞTHΞЯSPHΞЯΞ")
```

콘솔을 사용하여 H/s(초당 해시 작업) 단위로 현재 해시 속도를 확인할 수도 있습니다.

```sh
eth.hashrate
 712000
```

일부 블록이 채굴된 후 etherbase 계정 잔액이 >0이 됩니다. etherbase가 로컬 계정이라고 가정합니다.

```sh
eth.getBalance(eth.coinbase).toNumber();
 '34698870000000'
```



Javascript 콘솔에서 다음 코드 스니펫을 사용하여 특정 채굴자(주소)가 어떤 블록을 채굴했는지 확인할 수도 있습니다.

```javascript
function minedBlocks(lastn, addr) {
  addrs = [];
  if (!addr) {
    addr = eth.coinbase;
  }
  limit = eth.blockNumber - lastn;
  for (i = eth.blockNumber; i >= limit; i--) {
    if (eth.getBlock(i).miner == addr) {
      addrs.push(i);
    }
  }
  return addrs;
}

// scans the last 1000 blocks and returns the blocknumbers of blocks mined by your coinbase
// (more precisely blocks the mining reward for which is sent to your coinbase).
minedBlocks(1000, eth.coinbase)[(352708, 352655, 352559)];
```

채굴된 블록이 표준 체인에서 재구성되면 에테르베이스 잔액이 변동합니다. 이는 로컬 Geth 노드가 자체 로컬 블록체인에 채굴된 블록을 포함할 때 블록 보상이 적용되기 때문에 계정 잔액이 더 높게 나타난다는 것을 의미합니다. 피어로부터 받은 정보로 인해 노드가 다른 버전의 체인으로 전환하면 해당 블록이 포함되지 않을 수 있으며 블록 보상이 적용되지 않습니다.

로그에는 5개의 블록 후에 확인된 로컬 채굴 블록이 표시됩니다.

### &#x20;<a href="#summary" id="summary"></a>
