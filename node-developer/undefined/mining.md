# Mining

### &#x20;<a href="#summary" id="summary"></a>

블록체인은 개별 노드가 유효한 블록을 생성하고 블록을 확인하고 자신의 로컬 데이터베이스에 추가하는 동료에게 배포할 때 성장합니다.

블록을 추가하는 노드는 이더 지급으로 보상을 받습니다. 이더리움 메인넷에서 지분 증명 합의 엔진은 각 블록을 생성할 노드를 무작위로 선택합니다.

이더리움이 항상 이런 식으로 보호되는 것은 아닙니다. 원래는 작업 증명 기반 합의 메커니즘이 대신 사용되었습니다. 작업 증명 하에서 블록 생산자는 각 슬롯에서 무작위로 선택되지 않습니다. 대신 그들은 블록을 추가할 권리를 놓고 경쟁합니다. 무차별 대입 계산을 통해서만 찾을 수 있는 특정 값을 가장 빨리 계산하는 노드는 블록을 추가하는 노드입니다. 노드가 이 값을 계산하여 에너지를 소비했음을 입증할 수 있는 경우에만 다른 노드에서 해당 블록을 수락합니다. 작업 증명을 사용하여 블록을 생성하고 보호하는 이 프로세스를 "채굴"이라고 합니다.

Ethereum 노드에서 사용하는 특정 알고리즘("Ethash")에 대한 세부 정보를 포함하여 채굴에 대한 더 많은 정보는 [ethereum.org](https://ethereum.org/en/developers/docs/consensus-mechanisms/pow/mining-algorithms/ethash) 에서 확인할 수 있습니다 .



### 요약 <a href="#summary" id="summary"></a>

이 페이지는 Geth를 마이닝 노드로 시작하는 방법을 설명합니다. 마이닝은 CPU(이 경우 Geth의 내장 마이너를 사용할 수 있음) 또는 타사 소프트웨어가 필요한 GPU에서 수행할 수 있습니다. 마이닝은 **더 이상 Ethereum Mainnet을 보호하는 데 사용되지 않습니다** .



### Geth로 CPU 마이닝 <a href="#cpu-mining-with-geth" id="cpu-mining-with-geth"></a>

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
