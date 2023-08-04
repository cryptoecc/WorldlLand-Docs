# Peer

The WorldLand blockchain network is a peer-to-peer network. When an ETH-ECC node is running, the node runs a peer discovery protocol. ETH-ECC nodes will continue to try to connect to other EVM-compatible nodes on the internet. Upon discovering an EVM-compatible node, the nodes exchange protocol details. If both nodes use the Worldland blockchain protocol, the nodes exchange blockchain data.



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
$ ./worldland -bootnodes enode://pubkey1@ip1:port1,enode://pubkey2@ip2:port2,enode://pubkey3@ip3:port3
```



There are cases where the discovery process is unnecessary, such as when running local tests on the Gwangju or Seoul networks where bootnodes exist. In this case, you can disable the discovery protocol on startup via the `-nodiscover` option.

```
$ ./worldland -nodiscover
```



### Check connection

In the net module of the JSON-RPC API, there are two commands to check node connectivity. The `net.listening` command returns whether a node is currently listening for peer connection requests from other peers.

```
> net.listening
true
```



The `net.peercount` command returns the number of active peers among the peers of the current node.

```
> net.peerCount
3
```



You can get detailed information about peers through the admin module of the JSON-RPC API.&#x20;

The `admin.peers` command can get detailed information about all currently connected peers. You can get most of the information such as ip address, current protocol status, enode information, etc.

```sh
> admin.peers
[{
  caps: ["eth/66", "eth/67", "snap/1"],
  enode: "enode://4f4be8c67ac7b1fcfceb21a374a62c68f7f0528988f3b3d322bd6d94aeb745667f0c8e847881bbaeeba52eb1d346166301243222d5e22dd16ce70c57214178ca@43.200.52.189:30303",
  enr: "enr:-KO4QOF-XTPpf4Hl4jY--o7eJHFAuIKEb38ePS9O6IB8w7OhLWrE3N7xBEjYNLqIeNfva3knzI0EeYdMd2lmsB9bIGKGAYmqPaspg2V0aMfGhGInNlqAgmlkgnY0gmlwhCvINL2Jc2VjcDI1NmsxoQJPS-jGesex_PzrIaN0pixo9_BSiYjzs9MivW2UrrdFZoRzbmFwwIN0Y3CCdl-DdWRwgnZf",
  id: "2eb88a8ad5e462651f93397b257defd3c5dfd62e46dbffdd2f34bc1fe0501b7a",
  name: "Worldland/v1.0.0-unstable-af278478-20230731/linux-amd64/go1.20.6",
  network: {
    inbound: false,
    localAddress: "192.168.77.3:36708",
    remoteAddress: "43.200.52.189:30303",
    static: false,
    trusted: false
  },
  protocols: {
    eth: {
      difficulty: 5844127984,
      head: "0x3b74ea90a7fbf835c452da8d618e3c1d615ef7e7eec7a9c2b24d4cd34472321a",
      version: 67
    },
    snap: {
      version: 1
    }
  }
},
{
  caps: ["eth/66", "eth/67", "snap/1"],
  enode: "enode://bbbf2734ce12b7aa258dd1e92e9cec7ea6b2ca6766f5741272c934904f3d182e08688aef3a368684c4c06b6adc2711c51e517bb9033824b2816c9d038c256cf9@3.36.252.183:30303",
  enr: "enr:-KO4QNVFsMeW7bR0-6XzVokCwXK6cHD9rPqbXJ0AVi4XWrnQX0-XwnzUKijecYJmxbrc32Z2mB-jQwqsngAdbnKoP6SGAYmqQOqTg2V0aMfGhGInNlqAgmlkgnY0gmlwhAMk_LeJc2VjcDI1NmsxoQO7vyc0zhK3qiWN0ekunOx-prLKZ2b1dBJyyTSQTz0YLoRzbmFwwIN0Y3CCdl-DdWRwgnZf",
  id: "6fc0c411f0c7436b225cf4451535a87c502a09b01535c4d816a504d014c5b99e",
  name: "Worldland/v1.0.0-unstable-af278478-20230731/linux-amd64/go1.20.6",
  network: {
    inbound: false,
    localAddress: "192.168.77.3:56906",
    remoteAddress: "3.36.252.183:30303",
    static: false,
    trusted: false
  },
  protocols: {
    eth: {
      difficulty: 5846302836,
      head: "0xc7dfff5a4fa511fe835716604de15959e198c7ebb9dbcd3e1c347bf9d47ff34a",
      version: 67
    },
    snap: {
      version: 1
    }
  }
},
{
    caps: ["eth/66", "eth/67", "snap/1"],
    enode: "enode://911771c7894782bced03377a13f1d8a4e8450d05e03eabab1d6daae70e1b91b6074c346d42ac4fae53d98d273efedd6cdd37d2f6715302de9736b29cc4aa7da2@13.250.246.202:30303",
    enr: "enr:-KO4QG4exbZWnaR2Lznmd3g0rLLz815ZKWnLck9gtEp3kJ2FTP77AY4cJAPXIHuEB3IwOOvl1JQpudD1zCAG9KMw_KKGAYmqRHwLg2V0aMfGhGInNlqAgmlkgnY0gmlwhA369sqJc2VjcDI1NmsxoQKRF3HHiUeCvO0DN3oT8dik6EUNBeA-q6sdbarnDhuRtoRzbmFwwIN0Y3CCdl-DdWRwgnZf",
    id: "9918c39af25a0dab9228a4dac9e0f8bf2eee1d4b004a63d6e070603c3d0c1d66",
    name: "Worldland/v1.0.0-unstable-af278478-20230731/linux-amd64/go1.20.6",
    network: {
      inbound: false,
      localAddress: "192.168.77.3:36394",
      remoteAddress: "13.250.246.202:30303",
      static: false,
      trusted: false
    },
    protocols: {
      eth: {
        difficulty: 5843979192,
        head: "0xd92932e41d3f861314fe8414a01ac02c309f7a6979295699a5a08e141071a932",
        version: 67
      },
      snap: {
        version: 1
      }
    }
}]
```



Also, node information of the local node can be obtained through the management module.&#x20;

The `admin.nodeInfo` command returns detailed node information of the local node.

```sh
> admin.nodeInfo
{ 
  enode: "enode://004d32a9d7833edda6b2d47e89705187ef791930410c6c88c3b169ad80b4031a4c7e26b3bbe8fae535088b1efae43fd968f53e2658105bd691472336c9713c15@211.171.40.162:30303",
  enr: "enr:-KO4QO0C-Z3ZeIwaRuYwpLP9EKW1nOl3NHRdWvGMPXn3Pp9RFjH_9-rW9WWbIA6Y0ccKH2zG3cB3YrG5bUJtUzbY9BSGAYmqT6yHg2V0aMfGhGInNlqAgmlkgnY0gmlwhNOrKKKJc2VjcDI1NmsxoQMATTKp14M-3aay1H6JcFGH73kZMEEMbIjDsWmtgLQDGoRzbmFwwIN0Y3CCdl-DdWRwgnZf",
  id: "d98855afc2b03c6183a9ce7bd252eaef19e0e5dd81c44f9398ea674e09dc35f0",
  ip: "211.171.40.162",
  listenAddr: "[::]:30303",
  name: "Worldland/v1.0.0-unstable-af278478-20230731/linux-amd64/go1.18.1",
  ports: {
    discovery: 30303,
    listener: 30303
  },
  protocols: {
    eth: {
      config: {
        HalvingEndTime: 25228800,
        berlinBlock: 0,
        byzantiumBlock: 0,
        chainId: 10395,
        constantinopleBlock: 0,
        daoForkSupport: true,
        eccpow: {},
        eip150Block: 0,
        eip150Hash: "0x0000000000000000000000000000000000000000000000000000000000000000",
        eip155Block: 0,
        eip158Block: 0,
        homesteadBlock: 0,
        istanbulBlock: 0,
        londonBlock: 0,
        petersburgBlock: 0,
        seoulBlock: 0,
        worldlandBlock: 0
      },
      difficulty: 5848298199,
      genesis: "0x64130a2624d46bda6aacf0c1ec34ab3d926e31b8438141a10e7412070064f0bf",
      head: "0x3cab1cccd90c7dab9d05f0b11168ab4a6d5c1faf1ba1de7e77e9f591af994173",
      network: 10395
    },
    snap: {}
  }
}
```



### Static Node <a href="#static-nodes" id="static-nodes"></a>

ETH-ECC 노드 사용자가 수동 추가를 통해 정적 노드를 추가할 수 있습니다. 정적 노드는 항상 연결이 유지되는 특정 피어를 말합니다. ETH-ECC 노드가 중지 후 다시 실행되더라도, 노드는 다시 정적 노드에 연결합니다. 정적 노드는 콘솔을 통해 직접 추가하거나, 커맨드 라인 명령을 통해서 추가할 수 있습니다.&#x20;





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

