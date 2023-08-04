# Peer

The WorldLand blockchain network is a peer-to-peer network. When an ETH-ECC node is running, the node runs a peer discovery protocol. ETH-ECC nodes will continue to try to connect to other EVM-compatible nodes on the internet. Upon discovering an EVM-compatible node, the nodes exchange protocol details. If both nodes use the Worldland blockchain protocol, the nodes exchange blockchain data.

EVM-compatible

### Bootnodes

In order for a new node to join the WorldLand network, it must discover the WorldLand node through the peer discovery protocol. However, it is not easy to quickly find a node without any clues on the vast internet. WorldLand supports new nodes through bootstrap nodes (bootnodes). The bootnode is hardcoded inside the ETH-ECC code. When an ETH-ECC node starts up, it automatically tries to connect to a set of bootnodes. Below is currently hardcoded. This is a list of boot nodes in the Seoul network and the Gwangju network.

[ETH-ECC/params/bootnodes.go](https://github.com/cryptoecc/ETH-ECC/blob/dbbde3d95e52d827fe294035270ecc1ca684f3d2/params/bootnodes.go#L85)

```
// SeoulBootnodes are the enode URLs of the P2P bootstrap nodes running on the
// Seoul network.
var SeoulBootnodes = []string{
	"enode://00de00356ccba2b6960fb0fe29d596388494efd4f889772e5b86f45cf52055c343e35daa2a8fe5f02e7c239056ddfb4e143d7488dc0831b00f018f7ce0ddab4b@3.39.197.118:30303",
	"enode://7b32ddd47f9db43dd660ae3e2cb05ebd36d1092aa1a3ee31a9090c7d459ac26dbc2352693d6217d466ad8dfdf09fe69a48265d2a53a7dc18a931347ad6a481dd@3.36.252.183:30303",
	"enode://6477bc373216b8a59f59532ae01461f69f6ec88ec5ba81d293026089d973386d02f43004db1db5939532617c3dc20dd1f05c3dbd81c4fb23efedefb6129a1fb9@13.250.246.202:30303",
}

// Gwangju Bootnodes are the enode URLs of the P2P bootstrap nodes running on the
// Gwangju network.
var GwangjuBootnodes = []string{
	"enode://4f4be8c67ac7b1fcfceb21a374a62c68f7f0528988f3b3d322bd6d94aeb745667f0c8e847881bbaeeba52eb1d346166301243222d5e22dd16ce70c57214178ca@43.200.52.189:30303",
	"enode://bbbf2734ce12b7aa258dd1e92e9cec7ea6b2ca6766f5741272c934904f3d182e08688aef3a368684c4c06b6adc2711c51e517bb9033824b2816c9d038c256cf9@3.36.252.183:30303",
	"enode://911771c7894782bced03377a13f1d8a4e8450d05e03eabab1d6daae70e1b91b6074c346d42ac4fae53d98d273efedd6cdd37d2f6715302de9736b29cc4aa7da2@13.250.246.202:30303",
}
```



Bootnodes can also be specified at startup by supplying the `--bootnode` flag with comma-separated bootnode addresses in enodes format. for example:

```sh
$ ./worldland --bootnodes enode://pubkey1@ip1:port1,enode://pubkey2@ip2:port2,enode://pubkey3@ip3:port3
```



There are cases where the discovery process is unnecessary, such as when running local tests on the Gwangju or Seoul networks where bootnodes exist. In this case, you can disable the discovery protocol on startup via the `-nodiscover` option.

```
$ ./worldland -nodiscover
```





### 연결 문제 <a href="#connectivity-problems" id="connectivity-problems"></a>

Geth가 단순히 피어에 연결하지 못하는 경우가 있습니다. 이에 대한 일반적인 이유는 다음과 같습니다.

* 현지 시간이 정확하지 않을 수 있습니다. Ethereum 네트워크에 참여하려면 정확한 시계가 필요합니다. 로컬 시계는 sudo ntpdate -s time.nist.gov (운영 체제에 따라 다름) 와 같은 명령을 사용하여 다시 동기화할 수 있습니다 .
* 일부 방화벽 구성은 UDP 트래픽을 금지할 수 있습니다. 정적 노드 기능 또는 콘솔의 admin.addPeer()를 사용하여 연결을 수동으로 구성할 수 있습니다.

### 연결 확인 <a href="#checking-connectivity" id="checking-connectivity"></a>

net 모듈 에는 [대화형 Javascript 콘솔](https://geth.ethereum.org/docs/interacting-with-geth/javascript-console) 에서 노드 연결을 확인할 수 있는 두 가지 속성이 있습니다 . 이들은 Geth 노드가 인바운드 요청을 수신하는지 여부를 보고하는 net.listening 과 노드가 연결된 활성 피어 수를 반환하는 peerCount입니다 .

```javascript
> net.listening
true

> net.peerCount
4
```

관리 모듈 의 기능은 IP 주소, 포트 번호, 지원되는 프로토콜 등 연결된 피어에 대한 자세한 정보를 제공합니다. admin.peers를 호출하면 연결된 모든 피어에 대해 이 정보가 반환됩니다.

```sh
> admin.peers
[{
  ID: 'a4de274d3a159e10c2c9a68c326511236381b84c9ec52e72ad732eb0b2b1a2277938f78593cdbe734e6002bf23114d434a085d260514ab336d4acdc312db671b',
  Name: 'Geth/v0.9.14/linux/go1.4.2',
  Caps: 'eth/60',
  RemoteAddress: '5.9.150.40:30301',
  LocalAddress: '192.168.0.28:39219'
}, {
  ID: 'a979fb575495b8d6db44f750317d0f4622bf4c2aa3365d6af7c284339968eef29b69ad0dce72a4d8db5ebb4968de0e3bec910127f134779fbcb0cb6d3331163c',
  Name: 'Geth/v0.9.15/linux/go1.4.2',
  Caps: 'eth/60',
  RemoteAddress: '52.16.188.185:30303',
  LocalAddress: '192.168.0.28:50995'
}, {
  ID: 'f6ba1f1d9241d48138136ccf5baa6c2c8b008435a1c2bd009ca52fb8edbbc991eba36376beaee9d45f16d5dcbf2ed0bc23006c505d57ffcf70921bd94aa7a172',
  Name: 'pyethapp_dd52/v0.9.13/linux2/py2.7.9',
  Caps: 'eth/60, p2p/3',
  RemoteAddress: '144.76.62.101:30303',
  LocalAddress: '192.168.0.28:40454'
}, {
  ID: 'f4642fa65af50cfdea8fa7414a5def7bb7991478b768e296f5e4a54e8b995de102e0ceae2e826f293c481b5325f89be6d207b003382e18a8ecba66fbaf6416c0',
  Name: '++eth/Zeppelin/Rascal/v0.9.14/Release/Darwin/clang/int',
  Caps: 'eth/60, shh/2',
  RemoteAddress: '129.16.191.64:30303',
  LocalAddress: '192.168.0.28:39705'
} ]

```

관리 모듈 에는 피어가 아닌 로컬 노드에 대한 정보를 수집하는 기능도 포함되어 있습니다. 예를 들어 admin.nodeInfo는 로컬 노드의 이름 및 연결 세부 정보를 반환합니다.

```sh
> admin.nodeInfo
{
  Name: 'Geth/v0.9.14/darwin/go1.4.2',
  NodeUrl: 'enode://3414c01c19aa75a34f2dbd2f8d0898dc79d6b219ad77f8155abf1a287ce2ba60f14998a3a98c0cf14915eabfdacf914a92b27a01769de18fa2d049dbf4c17694@[::]:30303',
  NodeID: '3414c01c19aa75a34f2dbd2f8d0898dc79d6b219ad77f8155abf1a287ce2ba60f14998a3a98c0cf14915eabfdacf914a92b27a01769de18fa2d049dbf4c17694',
  IP: '::',
  DiscPort: 30303,
  TCPPort: 30303,
  Td: '2044952618444',
  ListenAddr: '[::]:30303'
}
```

### 정적 노드 <a href="#static-nodes" id="static-nodes"></a>

Geth는 정적 노드도 지원합니다. 정적 노드는 항상 연결된 특정 피어입니다. Geth는 다시 시작되면 이러한 피어에 자동으로 다시 연결됩니다. 특정 노드는 구성 파일에 enode 주소를 추가하여 정적 노드로 정의됩니다. 이 구성 파일을 만드는 가장 쉬운 방법은 다음을 실행하는 것입니다.

```sh
geth --datadir <datadir> dumpconfig > config.toml
```

이렇게 하면 현재 디렉터리에 config.toml이 생성됩니다 . 그런 다음 정적 노드에 대한 enode 주소를 config.toml 의 Node.P2P 섹션 에 있는 StaticNodes 필드 에 목록으로 추가할 수 있습니다 . Geth가 시작되면 --config config.toml 을 전달합니다 . config.toml 의 관련 행은 다음과 같습니다.

```toml
StaticNodes = ["enode://f4642fa65af50cfdea8fa7414a5def7bb7991478b768e296f5e4a54e8b995de102e0ceae2e826f293c481b5325f89be6d207b003382e18a8ecba66fbaf6416c0@33.4.2.1:30303"]
```

\--config를 전달하면 Geth가 이 파일에서 구성 값을 가져오도록 지시하므로 Geth를 시작하기 전에 config.toml 의 다른 라인 도 올바르게 설정되었는지 확인하십시오. 전체 config.toml 파일의 예는 [여기에서](https://gist.github.com/jmcook1186/16db2f0feddb4bd0581ebb9ba867a47a) 찾을 수 있습니다 .

admin.addPeer() 에 enode 주소를 전달하여 Javascript 콘솔에서 런타임에 정적 노드를 추가할 수도 있습니다 .

```javascript
admin.addPeer(
  'enode://f4642fa65af50cfdea8fa7414a5def7bb7991478b768e296f5e4a54e8b995de102e0ceae2e826f293c481b5325f89be6d207b003382e18a8ecba66fbaf6416c0@33.4.2.1:30303'
);
```

### 피어 제한 <a href="#peer-limit" id="peer-limit"></a>

노드 실행과 관련된 계산 및 대역폭 비용을 제한하기 위해 Geth가 연결할 피어 수를 제한하는 것이 때때로 바람직합니다. 기본적으로 제한은 피어 50개이지만 --maxpeers 에 값을 전달하여 업데이트할 수 있습니다 .

```sh
geth <otherflags> --maxpeers 15
```



### 요약 <a href="#summary" id="summary"></a>

Geth는 기본적으로 Ethereum Mainnet에 연결됩니다. 그러나 이 동작은 명령줄 플래그와 파일의 조합을 사용하여 변경할 수 있습니다. 이 페이지에서는 Geth 노드를 Ethereum, 공용 테스트넷 및 사설 네트워크에 연결하는 데 사용할 수 있는 다양한 옵션을 설명했습니다. 지분 증명 네트워크(예: Ethereum Mainnet, Goerli, Sepolia)에 연결하려면 합의 클라이언트도 필요합니다.

