# Admin

admin API 는 네트워크 피어 및 RPC 끝점 관리를 포함하되 이에 국한되지 않는 Geth 인스턴스에 대한 세밀한 제어를 허용하는 여러 비표준 RPC 방법에 대한 액세스를 제공합니다.

### admin\_addPeer <a href="#admin-addpeer" id="admin-addpeer"></a>

addPeer 관리 메소드 는 추적된 정적 노드 목록에 새 원격 노드를 추가하도록 요청합니다. 노드는 항상 이러한 노드에 대한 연결을 유지하려고 시도하며 원격 연결이 끊어지면 가끔씩 다시 연결합니다.

이 메서드는 단일 인수, 추적을 시작할 원격 피어의 [enode](https://ethereum.org/en/developers/docs/networking-layer/network-addresses/#enode) URL을 수락하고 피어가 추적을 위해 수락되었는지 또는 일부 오류가 발생했는지 여부를 나타내는 BOOL을 반환합니다.

| 고객  | 메서드 호출                                   |
| --- | ---------------------------------------- |
| 가다  | admin.AddPeer(url 문자열) (부울, 오류)          |
| 콘솔  | admin.addPeer(URL)                       |
| RPC | {"방법": "admin\_addPeer", "매개변수": \[url]} |

#### 예 <a href="#example" id="example"></a>

```javascript
> admin.addPeer("enode://a979fb575495b8d6db44f750317d0f4622bf4c2aa3365d6af7c284339968eef29b69ad0dce72a4d8db5ebb4968de0e3bec910127f134779fbcb0cb6d3331163c@52.16.188.185:30303")
true
```

### admin\_addTrustedPeer <a href="#admin-addtrustedpeer" id="admin-addtrustedpeer"></a>

슬롯이 가득 차더라도 노드가 항상 연결할 수 있도록 예약된 신뢰할 수 있는 목록에 지정된 노드를 추가합니다. 피어가 목록에 성공적으로 추가되었는지 여부를 나타내는 BOOL을 반환합니다 .

| 고객  | 메서드 호출                                          |
| --- | ----------------------------------------------- |
| 콘솔  | admin.addTrustedPeer(url)                       |
| RPC | {"방법": "admin\_addTrustedPeer", "매개변수": \[URL]} |

### admin\_datadir <a href="#admin-datadir" id="admin-datadir"></a>

실행 중인 Geth 노드 가 현재 모든 데이터베이스를 저장하는 데 사용하는 절대 경로에 대해 datadir 관리 속성을 쿼리할 수 있습니다 .

| 고객  | 메서드 호출                     |
| --- | -------------------------- |
| 가다  | admin.Datadir() (문자열, 오류 ) |
| 콘솔  | admin.datadir              |
| RPC | {"방법": "admin\_datadir"}   |

#### 예 <a href="#example" id="example"></a>

```javascript
> admin.datadir
"/home/john/.ethereum"
```

### admin\_exportChain <a href="#admin-exportchain" id="admin-exportchain"></a>

현재 블록체인을 로컬 파일로 내보냅니다. 선택적으로 첫 번째 및 마지막 블록 번호를 사용하며, 이 경우 해당 범위의 블록만 내보냅니다. 작업이 성공했는지 여부를 나타내는 부울을 반환합니다.

| 고객  | 메서드 호출                                                       |
| --- | ------------------------------------------------------------ |
| 콘솔  | admin.exportChain(파일, 첫 번째, 마지막)                             |
| RPC | {"방법": "admin\_exportChain", "매개변수": \[문자열, uint64, uint64]} |

### admin\_importChain <a href="#admin-importchain" id="admin-importchain"></a>

로컬 파일에서 내보낸 블록 목록을 가져옵니다. 가져오기에는 블록을 처리하고 이를 정식 체인에 삽입하는 작업이 포함됩니다. 이 범위의 상위 블록 상태가 필요합니다. 작업이 성공했는지 여부를 나타내는 부울을 반환합니다.

| 고객  | 메서드 호출                                       |
| --- | -------------------------------------------- |
| 콘솔  | admin.importChain(파일)                        |
| RPC | {"방법": "admin\_importChain", "매개변수": \[문자열]} |

### admin\_nodeInfo <a href="#admin-nodeinfo" id="admin-nodeinfo"></a>

네트워킹 세분성에서 실행 중인 Geth 노드 에 대해 알려진 모든 정보에 대해 nodeInfo 관리 속성을 쿼리할 수 있습니다 . [여기에는 ÐΞVp2p](https://github.com/ethereum/devp2p/blob/master/caps/eth.md) P2P 오버레이 프로토콜 의 참가자인 노드 자체에 대한 일반 정보 와 실행 중인 각 애플리케이션 프로토콜(예: eth , les , shh , bzz )에 의해 추가된 특수 정보가 포함됩니다.

| 고객  | 메서드 호출                                 |
| --- | -------------------------------------- |
| 가다  | admin.NodeInfo() (\*p2p.NodeInfo, 오류 ) |
| 콘솔  | admin.nodeInfo                         |
| RPC | {"방법": "admin\_nodeInfo"}              |

#### 예 <a href="#example" id="example"></a>

```javascript
> admin.nodeInfo
{
  enode: "enode://44826a5d6a55f88a18298bca4773fca5749cdc3a5c9f308aa7d810e9b31123f3e7c5fba0b1d70aac5308426f47df2a128a6747040a3815cc7dd7167d03be320d@[::]:30303",
  id: "44826a5d6a55f88a18298bca4773fca5749cdc3a5c9f308aa7d810e9b31123f3e7c5fba0b1d70aac5308426f47df2a128a6747040a3815cc7dd7167d03be320d",
  ip: "::",
  listenAddr: "[::]:30303",
  name: "Geth/v1.5.0-unstable/linux/go1.6",
  ports: {
    discovery: 30303,
    listener: 30303
  },
  protocols: {
    eth: {
      difficulty: 17334254859343145000,
      genesis: "0xd4e56740f876aef8c010b86a40d5f56745a118d0906a34e69aec8c0db1cb8fa3",
      head: "0xb83f73fbe6220c111136aefd27b160bf4a34085c65ba89f24246b3162257c36a",
      network: 1
    }
  }
}
```

### admin\_peer이벤트 <a href="#admin-peerevents" id="admin-peerevents"></a>

PeerEvents는 노드의 p2p 서버에서 피어 이벤트를 수신하는 [RPC 구독을 생성합니다. ](https://geth.ethereum.org/docs/interacting-with-geth/rpc/pubsub)서버에서 발생하는 이벤트 유형은 다음과 같습니다.

* add : 피어가 추가될 때 발생
* drop : 피어가 삭제될 때 발생합니다.
* msgsend : 메시지가 피어에게 성공적으로 전송되었을 때 방출됩니다.
* msgrecv : 피어로부터 메시지를 수신할 때 발생합니다.

### admin\_peers <a href="#admin-peers" id="admin-peers"></a>

네트워킹 세분성에서 연결된 원격 노드에 대해 알려진 모든 정보에 대해 피어 관리 속성을 쿼리할 수 있습니다. [여기에는 ÐΞVp2p](https://github.com/ethereum/devp2p/blob/master/caps/eth.md) P2P 오버레이 프로토콜 의 참가자인 노드 자체에 대한 일반 정보 와 실행 중인 각 애플리케이션 프로토콜(예: eth , les , shh , bzz )에 의해 추가된 특수 정보가 포함됩니다.

| 고객  | 메서드 호출                                 |
| --- | -------------------------------------- |
| 가다  | admin.Peers() (\[]\*p2p.PeerInfo, 오류 ) |
| 콘솔  | admin.peers                            |
| RPC | {"방법": "admin\_peers"}                 |

#### 예 <a href="#example" id="example"></a>

```javascript
> admin.peers
[{
    caps: ["eth/61", "eth/62", "eth/63"],
    id: "08a6b39263470c78d3e4f58e3c997cd2e7af623afce64656cfc56480babcea7a9138f3d09d7b9879344c2d2e457679e3655d4b56eaff5fd4fd7f147bdb045124",
    name: "Geth/v1.5.0-unstable/linux/go1.5.1",
    network: {
      localAddress: "192.168.0.104:51068",
      remoteAddress: "71.62.31.72:30303"
    },
    protocols: {
      eth: {
        difficulty: 17334052235346465000,
        head: "5794b768dae6c6ee5366e6ca7662bdff2882576e09609bf778633e470e0e7852",
        version: 63
      }
    }
}, /* ... */ {
    caps: ["eth/61", "eth/62", "eth/63"],
    id: "fcad9f6d3faf89a0908a11ddae9d4be3a1039108263b06c96171eb3b0f3ba85a7095a03bb65198c35a04829032d198759edfca9b63a8b69dc47a205d94fce7cc",
    name: "Geth/v1.3.5-506c9277/linux/go1.4.2",
    network: {
      localAddress: "192.168.0.104:55968",
      remoteAddress: "121.196.232.205:30303"
    },
    protocols: {
      eth: {
        difficulty: 17335165914080772000,
        head: "5794b768dae6c6ee5366e6ca7662bdff2882576e09609bf778633e470e0e7852",
        version: 63
      }
    }
}]
```

### admin\_removePeer <a href="#admin-removepeer" id="admin-removepeer"></a>

연결이 존재하는 경우 원격 노드에서 연결을 끊습니다. 유효성 검사가 성공했음을 나타내는 부울을 반환합니다. true 값이 반드시 연결이 끊어진 연결이 있음을 의미하지는 않습니다.

| 고객  | 메서드 호출                                      |
| --- | ------------------------------------------- |
| 콘솔  | admin.removePeer(url)                       |
| RPC | {"방법": "admin\_removePeer", "매개변수": \[문자열]} |

### admin\_removeTrustedPeer <a href="#admin-removetrustedpeer" id="admin-removetrustedpeer"></a>

신뢰할 수 있는 피어 세트에서 원격 노드를 제거하지만 자동으로 연결을 끊지는 않습니다. 유효성 검사가 성공했음을 나타내는 부울을 반환합니다.

| 고객  | 메서드 호출                                             |
| --- | -------------------------------------------------- |
| 콘솔  | admin.removeTrustedPeer(URL)                       |
| RPC | {"방법": "admin\_removeTrustedPeer", "매개변수": \[문자열]} |

### admin\_startHTTP <a href="#admin-starthttp" id="admin-starthttp"></a>

startHTTP 관리 메소드는 HTTP 기반 JSON-RPC [API 웹 서버 ](https://geth.ethereum.org/docs/interacting-with-geth/rpc)를 시작하여 클라이언트 요청을 처리합니다. 모든 매개변수는 선택적입니다.

* host : 리스너 소켓을 여는 네트워크 인터페이스 (기본값은 "localhost" )
* port : 리스너 소켓을 여는 네트워크 포트 (기본값은 8545 )
* cors : 사용할 [교차 출처 리소스 공유 헤더(기본값은 ](https://en.wikipedia.org/wiki/Cross-origin\_resource\_sharing)"" )
* apis : 이 인터페이스를 통해 제공할 API 모듈(기본값은 "eth,net,web3" )

이 메서드는 HTTP RPC 수신기가 열렸는지 여부를 지정하는 부울 플래그를 반환합니다. 한 번에 하나의 HTTP 끝점만 활성화할 수 있습니다.

| 고객  | 메서드 호출                                                                          |
| --- | ------------------------------------------------------------------------------- |
| 가다  | admin.StartHTTP(호스트 \*문자열, 포트 \*rpc.HexNumber, cors \*문자열, apis \*문자열) (부울, 오류) |
| 콘솔  | admin.startHTTP(호스트, 포트, cors, apis)                                            |
| RPC | {"방법": "admin\_startHTTP", "매개 변수": \[호스트, 포트, cors, apis]}                     |

#### 예 <a href="#example" id="example"></a>

```javascript
> admin.startHTTP("127.0.0.1", 8545)
true
```

### admin\_startWS <a href="#admin-startws" id="admin-startws"></a>

startWS 관리 메소드는 WebSocket 기반 JSON RPC API 웹 서버를 시작하여 클라이언트 [요청](https://www.jsonrpc.org/specification) 을 처리합니다. 모든 매개변수는 선택적입니다.

* host : 리스너 소켓을 여는 네트워크 인터페이스 (기본값은 "localhost" )
* port : 리스너 소켓을 여는 네트워크 포트 (기본값은 8546 )
* cors : 사용할 [교차 출처 리소스 공유 헤더(기본값은 ](https://en.wikipedia.org/wiki/Cross-origin\_resource\_sharing)"" )
* apis : 이 인터페이스를 통해 제공할 API 모듈(기본값은 "eth,net,web3" )

이 메서드는 WebSocket RPC 수신기가 열렸는지 여부를 지정하는 부울 플래그를 반환합니다. 언제든지 하나의 WebSocket 끝점만 활성화할 수 있습니다.

| 고객  | 메서드 호출                                                                        |
| --- | ----------------------------------------------------------------------------- |
| 가다  | admin.StartWS(호스트 \*문자열, 포트 \*rpc.HexNumber, cors \*문자열, apis \*문자열) (부울, 오류) |
| 콘솔  | admin.startWS(호스트, 포트, cors, apis)                                            |
| RPC | {"방법": "admin\_startWS", "매개변수": \[호스트, 포트, cors, API]}                       |

#### 예 <a href="#example" id="example"></a>

```javascript
> admin.startWS("127.0.0.1", 8546)
true
```

### admin\_stopHTTP <a href="#admin-stophttp" id="admin-stophttp"></a>

stopHTTP 관리 메소드 는 현재 열려 있는 HTTP RPC 끝점을 닫습니다. 노드에는 단일 HTTP 엔드포인트만 실행될 수 있으므로 이 메서드는 매개변수를 사용하지 않고 엔드포인트가 닫혔는지 여부에 관계없이 부울을 반환합니다.

| 고객  | 메서드 호출                     |
| --- | -------------------------- |
| 가다  | admin.StopHTTP() (부울, 오류 ) |
| 콘솔  | admin.stopHTTP()           |
| RPC | {"방법": "admin\_stopHTTP"   |

#### 예 <a href="#example" id="example"></a>

```javascript
> admin.stopHTTP()
true
```

### admin\_stopWS <a href="#admin-stopws" id="admin-stopws"></a>

stopWS 관리 메소드 는 현재 열려 있는 WebSocket RPC 끝점을 닫습니다. 노드에는 단일 WebSocket 엔드포인트만 실행될 수 있으므로 이 메서드는 매개변수를 사용하지 않고 엔드포인트가 닫혔는지 여부에 관계없이 부울을 반환합니다.

| 고객  | 메서드 호출                   |
| --- | ------------------------ |
| 가다  | admin.StopWS() (부울, 오류 ) |
| 콘솔  | admin.stopWS()           |
| RPC | {"방법": "admin\_stopWS"   |

#### 예 <a href="#example" id="example"></a>

```javascript
> admin.stopWS()
true
```
