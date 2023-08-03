# Security

### 네트워킹 보안 <a href="#networking-security" id="networking-security"></a>

로컬 시스템의 방화벽 설정은 다음과 같아야 합니다.

* 8545 에 대한 모든 트래픽 또는 노드에 대한 JSON-RPC 요청에 대해 정의된 모든 사용자 정의 포트(명시적으로 정의된 신뢰할 수 있는 시스템의 트래픽 제외)를 차단합니다.
* TCP 30303 또는 P2P 통신을 위해 정의된 사용자 지정 포트 에서 트래픽을 허용합니다 . 이렇게 하면 노드가 피어에 연결할 수 있습니다.
* UDP 30303 또는 P2P 통신을 위해 정의된 사용자 지정 포트 에서 트래픽을 허용합니다 . 이를 통해 노드 검색이 가능합니다.

## **노드 구성** <a href="#f904" id="f904"></a>

### **절대 이렇게 하지 마세요!!!** <a href="#fb4b" id="fb4b"></a>

GETH 노드에서 RPC 액세스를 활성화할 때 잠금 해제된 계정으로 RPC에 대한 외부 액세스를 허용해서는 안 됩니다. 예를 들어

```
$ geth — rpc — rpcaddr 0.0.0.0 — rpcport 8545 — rpcapi "db, eth, net, web3, personal" — ipcapi "admin,eth,debug,personal,web3" — <addrs> 잠금 해제
```

기본적으로 이더리움 계정에 대한 외부 액세스를 허용하고 있으며 계정 잠금을 해제하면 공격자가 지갑에 저장된 이더를 쉽게 전송할 수 있습니다.

이 오류로 인해 사람들이 해킹당하는 예

* [https://ethereum.stackexchange.com/questions/3887/how-to-reduce-the-chances-of-your-ethereum-wallet-getting-hacked?utm\_medium=organic\&utm\_source=google\_rich\_qa\&utm\_campaign=google\_rich\_qa](https://ethereum.stackexchange.com/questions/3887/how-to-reduce-the-chances-of-your-ethereum-wallet-getting-hacked?utm\_medium=organic\&utm\_source=google\_rich\_qa\&utm\_campaign=google\_rich\_qa)
* 그리고 내 친구 :)

[https://medium.com/coinmonks/securing-your-ethereum-nodes-from-hackers-8b7d5bac8986](https://medium.com/coinmonks/securing-your-ethereum-nodes-from-hackers-8b7d5bac8986)

[https://medium.com/coinmonks/securing-your-ethereum-nodes-from-hackers-8b7d5bac8986](https://medium.com/coinmonks/securing-your-ethereum-nodes-from-hackers-8b7d5bac8986)

[https://ethereum.stackexchange.com/questions/32619/is-it-secure-to-run-public-ethereum-node](https://ethereum.stackexchange.com/questions/32619/is-it-secure-to-run-public-ethereum-node)

### 계정 보안 <a href="#account-security" id="account-security"></a>

계정 보안은 개인 키와 계정 암호를 백업하고 적이 액세스할 수 없도록 유지하는 것입니다. 이것은 사용자가 책임지는 것입니다. Geth는 계정 암호를 사용하여 잠금 해제된 키에 대해 암호화된 저장소를 제공합니다. 키 파일이나 암호를 분실하면 계정에 액세스할 수 없으며 자금은 사실상 영원히 손실됩니다. 암호화되지 않은 키에 대한 액세스 권한을 적이 획득한 경우 계정과 관련된 모든 자금을 제어할 수 있습니다.

Geth에는 계정 관리 도구가 내장되어 있습니다. 그러나 Clef는 외부 계정 관리 및 서명 도구로 권장됩니다. Geth에서 분리하여 실행할 수 있으며 VM 또는 보안 USB 드라이브와 같은 전용 보안 외부 하드웨어에서도 실행할 수 있습니다. 미리 정의된 특정 규칙이 구현된 경우를 제외하고 민감한 데이터를 다루는 모든 작업을 사용자가 수동으로 검토해야 하므로 이는 모범 사례로 간주됩니다. 서명은 노드에 대한 키 액세스를 제공하는 대신 Clef에 대해 로컬로 수행됩니다. Geth의 기본 제공 관리 도구는 가까운 시일 내에 더 이상 사용되지 않을 예정입니다.

**키 저장소와 암호를 안전하고 확실하게 백업하십시오!**
