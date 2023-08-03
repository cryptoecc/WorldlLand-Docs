# Server

Geth와 상호 작용하려면 특정 JSON-RPC API 메서드에 요청을 보내야 합니다. Geth는 모든 표준 [JSON-RPC API](https://github.com/ethereum/execution-apis) 끝점을 지원합니다. RPC 요청은 노드로 전송되어야 하며 응답은 일부 전송 프로토콜을 사용하여 클라이언트로 반환되어야 합니다. 이 페이지에서는 Geth에서 사용 가능한 전송 프로토콜에 대해 설명하고 사용자가 특정 사용자 시나리오에 대한 전송 프로토콜을 선택하는 데 필요한 정보를 제공합니다.

### 소개 <a href="#introduction" id="introduction"></a>

JSON-RPC는 여러 전송에서 제공됩니다. Geth는 HTTP, WebSocket 및 Unix 도메인 소켓을 통해 JSON-RPC를 지원합니다. 명령줄 플래그를 통해 전송을 활성화해야 합니다.

Ethereum JSON-RPC API는 이름 공간 시스템을 사용합니다. RPC 방법은 목적에 따라 여러 범주로 그룹화됩니다. 모든 메서드 이름은 네임스페이스, 밑줄 및 네임스페이스 내의 실제 메서드 이름으로 구성됩니다. 예를 들어 eth\_call 메서드는 eth 네임스페이스 에 있습니다 .

RPC 메서드에 대한 액세스는 네임스페이스별로 활성화할 수 있습니다. 사이드바에서 개별 네임스페이스에 대한 문서를 찾으십시오.

### 운송 <a href="#transports" id="transports"></a>

Geth에는 IPC, HTTP 및 Websocket의 세 가지 전송 프로토콜이 있습니다.

#### HTTP 서버 <a href="#http-server" id="http-server"></a>

[HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP) 는 클라이언트와 서버를 연결하는 단방향 전송 프로토콜입니다. 클라이언트는 서버에 요청을 보내고 서버는 클라이언트에 응답을 반환합니다. 주어진 요청에 대한 응답이 전송된 후 HTTP 연결이 닫힙니다.

HTTP는 모든 브라우저와 거의 모든 프로그래밍 툴체인에서 지원됩니다. 편재성으로 인해 Geth와 상호 작용하는 데 가장 널리 사용되는 전송 수단이 되었습니다. Geth에서 HTTP 서버를 시작하려면 --http 플래그를 포함합니다.

```sh
geth --http
```

다른 명령이 제공되지 않으면 Geth는 로컬 루프백 인터페이스(127.0.0.1)에서 연결을 수락하는 기본 동작으로 돌아갑니다. 기본 수신 포트는 8545입니다. IP 주소 및 수신 포트는 --http.addr 및 --http.port 플래그를 사용하여 사용자 정의할 수 있습니다.

```sh
geth --http --http.port 3334
```

모든 JSON-RPC 메서드 네임스페이스가 기본적으로 HTTP 요청에 대해 활성화되는 것은 아닙니다. 대신 Geth가 시작될 때 명시적으로 화이트리스트에 추가되어야 합니다. 화이트리스트에 없는 RPC 네임스페이스를 호출하면 -32602 코드와 함께 RPC 오류가 반환됩니다 .

기본 화이트리스트는 eth , net 및 web3 네임스페이스에 대한 액세스를 허용합니다. 디버깅( debug ) 과 같은 다른 API에 대한 액세스를 활성화하려면 --http.api 플래그를 사용하여 구성해야 합니다 . HTTP를 통해 이러한 API를 활성화하는 것은 이러한 방법에 대한 액세스가 공격 표면을 증가시키므로 **권장되지 않습니다 .**

```sh
geth --http --http.api eth,net,web3
```

HTTP 서버는 모든 로컬 애플리케이션에서 연결할 수 있으므로 웹 페이지에서 API를 오용하지 못하도록 서버에 추가 보호 기능이 내장되어 있습니다. [웹 페이지에서 API에 액세스하려면(예: 온라인 IDE, Remix](https://remix.ethereum.org/) 사용 ) Cross-Origin 요청을 수락하도록 서버를 구성해야 합니다. 이는 --http.corsdomain 플래그를 사용하여 수행됩니다.

```sh
geth --http --http.corsdomain https://remix.ethereum.org
```

\--http.corsdomain 명령은 모든 출처에서 RPC에 액세스할 수 있도록 하는 와일드카드도 허용합니다 .

```sh
--http.corsdomain '*'
```

#### 웹소켓 서버 <a href="#websockets-server" id="websockets-server"></a>

Websocket은 양방향 전송 프로토콜입니다. Websocket 연결은 명시적으로 종료될 때까지 클라이언트와 서버에서 유지됩니다. 대부분의 최신 브라우저는 Websocket을 지원하므로 도구가 훌륭합니다.

Websocket은 양방향이기 때문에 서버는 클라이언트에 이벤트를 푸시할 수 있습니다. [따라서 Websocket은 이벤트 구독과](https://geth.ethereum.org/docs/interacting-with-geth/rpc/pubsub) 관련된 사용 사례에 적합한 선택입니다 . Websocket의 또 다른 이점은 핸드셰이크 절차 후 개별 메시지의 오버헤드가 낮아 많은 수의 요청을 보내는 데 적합하다는 것입니다.

Geth의 WebSocket 끝점 구성은 HTTP 전송과 동일한 패턴을 따릅니다. --ws 플래그를 사용하여 WebSocket 액세스를 활성화할 수 있습니다 . 추가 정보가 제공되지 않으면 Geth는 포트 8546에서 Websocket을 설정하는 기본 동작으로 돌아갑니다. --ws.addr , --ws.port 및 --ws.api 플래그 를 사용하여 WebSocket 서버. 예를 들어 사용자 정의 포트 3334를 사용하고 eth , net 및 web3 네임스페이스를 화이트리스트에 추가하여 RPC용 Websocket 연결로 Geth를 시작하려면 다음을 수행하십시오.

```sh
geth --ws --ws.port 3334 --ws.api eth,net,web3
```

Cross-Origin 요청 보호는 WebSocket 서버에도 적용됩니다. --ws.origins 플래그를 사용하여 웹 페이지에서 서버에 액세스할 수 있습니다 .

```sh
geth --ws --ws.origins http://myapp.example.com
```

\--http.corsdomain 과 마찬가지로 와일드카드 --ws.origins '\*'를 사용하면 모든 출처에서 액세스할 수 있습니다.

**메모**

기본적으로 HTTP 또는 Websocket 액세스가 활성화되면(예: --http 또는 ws 플래그 전달 ) **계정 잠금 해제가 금지됩니다 .** 외부에 노출된 HTTP/WS 포트를 통해 노드에 접근하는 공격자가 잠금 해제된 계정을 제어할 수 있기 때문입니다. --allow-insecure-unlock 플래그를 포함하여 계정 잠금을 강제로 해제할 수 있지만 이는 안전하지 않으며 안전하게 사용하는 방법을 완전히 이해하는 전문가를 제외하고는 **권장되지 않습니다 .** 이것은 가상의 위험이 아닙니다. **공격할 http 지원 Ethereum 노드를 지속적으로 스캔하는 봇이 있습니다.**

#### IPC 서버 <a href="#ipc-server" id="ipc-server"></a>

IPC는 일반적으로 노드와 콘솔이 동일한 시스템에 존재하는 로컬 환경에서 사용할 수 있습니다. Geth는 노드와 콘솔 간의 연결을 구성하는 컴퓨터 로컬 파일 시스템( ipcpath )에 파이프를 생성합니다. geth.ipc 파일은 동일한 시스템 의 다른 프로세스에서 Geth와 상호 작용하는 데 사용할 수도 있습니다.

UNIX 기반 시스템(Linux, OSX)에서 IPC는 UNIX 도메인 소켓입니다. Windows에서 IPC는 명명된 파이프를 사용하여 제공됩니다. IPC 서버는 기본적으로 활성화되어 있으며 모든 JSON-RPC 네임스페이스에 액세스할 수 있습니다.

청취 소켓은 기본적으로 데이터 디렉토리에 배치됩니다. Linux 및 macOS에서 geth 소켓의 기본 위치는 다음과 같습니다.

```sh
~/.ethereum/geth.ipc
```

Windows에서 IPC는 명명된 파이프를 통해 제공됩니다. geth 파이프의 기본 위치는 다음과 같습니다.

```sh
\\.\pipe\geth.ipc
```

소켓의 위치는 --ipcpath 플래그를 사용하여 사용자 정의할 수 있습니다. --ipcdisable 플래그를 사용하여 IPC를 비활성화할 수 있습니다 .

### 전송 프로토콜 선택 <a href="#choosing-transport-protocol" id="choosing-transport-protocol"></a>

다음 표에는 사용자가 사용할 프로토콜에 대해 정보에 입각한 결정을 내릴 수 있도록 각 전송 프로토콜의 상대적인 강점과 약점이 요약되어 있습니다.

|                 | HTTP    | WS      | IPC     |
| --------------- | ------- | ------- | ------- |
| 이벤트 구독          | N       | **그리고** | **그리고** |
| 원격 연결           | **그리고** | **그리고** | N       |
| 메시지당 메타데이터 오버헤드 | 높은      | 낮은      | 낮은      |

일반적으로 IPC는 로컬 시스템의 상호 작용으로 제한되고 외부 트래픽에 노출될 수 없기 때문에 가장 안전합니다. 이벤트를 구독하는 데에도 사용할 수 있습니다. HTTP는 요청 간의 연결을 닫는 친숙하고 멱등적인 전송이므로 요청 수가 상당히 적은 경우 전체 오버헤드가 낮아질 수 있습니다. Websockets는 이벤트 구독 및 스트리밍을 활성화하고 메시지당 더 적은 오버헤드로 대량의 요청을 처리할 수 있는 지속적인 개방 채널을 제공합니다.

### &#x20;<a href="#engine-api" id="engine-api"></a>

### 요약 <a href="#summary" id="summary"></a>

Geth 노드에 대한 RPC 요청은 세 가지 다른 전송 프로토콜을 사용하여 만들 수 있습니다. 프로토콜은 해당 플래그를 사용하여 시작할 때 활성화됩니다. 전송 프로토콜의 올바른 선택은 특정 사용 사례에 따라 다릅니다.
