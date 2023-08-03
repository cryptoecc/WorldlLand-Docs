# Console

[Geth는 JSON-RPC-API](https://geth.ethereum.org/docs/interacting-with-geth/rpc) 에 정의된 대로 JSON 개체로 인코딩된 명령에 응답합니다 . Geth 사용자는 [Curl](https://github.com/curl/curl) 과 같은 도구를 사용하여 예를 들어 HTTP를 통해 이러한 지침을 직접 보낼 수 있습니다 . 아래 코드 스니펫은 HTTP 포트 8545 가 노출된 로컬 Geth 노드로 전송된 계정 잔액에 대한 요청을 보여줍니다 .

```sh
curl --data '{"jsonrpc":"2.0","method":"eth_getBalance", "params": ["0x9b1d35635cc34752ca54713bb99d38614f63c955", "latest"], "id":2}' -H "Content-Type: application/json" localhost:8545
```

이는 16진수 문자열로 표현된 값이 있는 JSON 개체이기도 한 결과를 반환합니다. 예를 들면 다음과 같습니다.

`{"id":2,"jsonrpc":"2.0","result":"0x1639e49bba16280000"}`

이것은 Geth와 상호 작용하는 낮은 수준의 다소 오류가 발생하기 쉬운 방법입니다. 대부분의 개발자는 값을 16진수 문자열에서 숫자로 변환하거나 에테르 단위(Wei, Gwei 등) 간 변환과 같은 지루하고 어색한 작업을 추상화하는 편리한 라이브러리를 사용하는 것을 선호합니다. 그러한 라이브러리 중 하나는 [Web3.js](https://web3js.readthedocs.io/en/v1.7.3/) 입니다 . Geth의 Javascript 콘솔의 목적은 Web3.js 라이브러리의 하위 집합을 사용하여 Geth 노드와 상호 작용할 수 있는 내장 환경을 제공하는 것입니다.

**메모**

Geth와 함께 제공되는 web3.js 버전은 공식 Web3.js 문서에서 최신 버전이 아닙니다. Geth Javascript 콘솔에서 사용할 수 없는 몇 가지 Web3.js 라이브러리가 있습니다. Web3.js 설명서에 설명되어 있지 않은 관리 API도 Geth 콘솔에 포함되어 있습니다. Geth 콘솔에서 사용할 수 있는 전체 라이브러리 목록은 [JSON-RPC API 페이지](https://geth.ethereum.org/docs/interacting-with-geth/rpc) 에서 볼 수 있습니다 .

### 콘솔 시작 <a href="#starting-the-console" id="starting-the-console"></a>

Geth 콘솔을 사용하여 대화식 세션을 시작하는 방법에는 두 가지가 있습니다. 첫 번째는 Geth가 시작될 때 콘솔 명령을 제공하는 것입니다. 이렇게 하면 노드가 시작되고 동일한 터미널에서 콘솔이 실행됩니다. 따라서 로그가 콘솔을 가리지 않도록 노드에서 로그를 억제하는 것이 편리합니다. 로그가 필요하지 않은 경우 dev/null 경로로 리디렉션하여 효과적으로 음소거할 수 있습니다. 또는 로그가 필요한 경우 텍스트 파일로 리디렉션할 수 있습니다. 로그에 제공되는 세부 정보 수준은 아래 예와 같이 --verbosity 플래그에 1-6 사이의 값을 제공하여 조정할 수 있습니다.

```sh
# to mute logs
geth <other flags> console 2> /dev/null

# to save logs to file
geth <other flags> console --verbosity 3 2> geth-logs.log
```

또는 Javascript 콘솔을 기존 Geth 인스턴스(예: 다른 터미널에서 실행 중이거나 원격으로 실행 중인 인스턴스)에 연결할 수 있습니다. 이 경우 geth 연결을 사용하여 Geth 노드에 연결된 Javascript 콘솔을 열 수 있습니다. 또한 콘솔을 노드에 연결하는 데 사용되는 방법을 정의해야 합니다. Geth는 웹 소켓, HTTP 또는 로컬 IPC를 지원합니다. HTTP 또는 Websocket을 사용하려면 시작 시 다음 플래그를 제공하여 노드에서 활성화해야 합니다.

```sh
# enable websockets
geth <other flags> --ws

# enable http
geth <other flags> --http
```

위의 명령은 기본 HTTP/WS 끝점을 사용하고 기본 JSON-RPC 라이브러리만 활성화합니다. 사용된 Websocket 또는 HTTP 끝점을 업데이트하거나 추가 라이브러리에 대한 지원을 추가하려면 다음과 같이 .addr .port 및 .api 플래그를 사용할 수 있습니다.

```sh
# define a custom http adress, custom http port and enable libraries
geth <other commands> --http --http.addr 192.60.52.21 --http.port 8552 --http.api eth,web3,admin

# define a custom Websockets address and enable libraries
geth <other commands> --ws --ws.addr 192.60.52.21 --ws.port 8552 --ws.api eth,web3,admin
```

**HTTP 또는 Websockets 액세스가 활성화되면** 기본적으로 계정 잠금 해제를 포함한 일부 기능이 금지된다는 점에 유의해야 합니다 . 이는 외부에 노출된 HTTP/WS 포트를 통해 노드에 접근한 공격자가 잠금 해제된 계정을 제어하기 때문입니다. 이것은 가상의 위험이 아닙니다. **공격하기 위해 http 지원 Ethereum 노드를 지속적으로 스캔하는 봇이 있습니다** .

IPC를 사용하여 Javascript 콘솔을 Geth 노드에 연결할 수도 있습니다. Geth가 시작되면 geth.ipc 파일이 자동으로 생성되어 데이터 디렉터리에 저장됩니다. 이 파일 또는 특정 ipc 파일에 대한 사용자 지정 경로는 다음과 같이 geth attach 에 전달할 수 있습니다.

```sh
geth attach datadir/geth.ipc
```

콘솔이 시작되면 다음과 같이 표시됩니다.

`Welcome to the Geth Javascript console! instance: Geth/v1.10.18-unstable-8d85a701-20220503/linux-amd64/go1.18.1 coinbase: 0x281aabb85c68e1638bb092750a0d9bb06ba103ee at block: 12305815 (Thu May 26 2022 16:16:00 GMT+0100 (BST)) datadir: /home/go-ethereum/data modules: admin:1.0 debug:1.0 eth:1.0 ethash:1.0 miner:1.0 net:1.0 rpc:1.0 txpool:1.0 web3:1.0 To exit, press ctrl-d or type exit >`

### 대화식 사용 <a href="#interactive-use" id="interactive-use"></a>

콘솔이 시작되면 Geth와 상호 작용하는 데 사용할 수 있습니다. 콘솔은 Javascript 및 전체 Geth [JSON-RPC API를](https://geth.ethereum.org/docs/interacting-with-geth/rpc) 지원합니다 . 예를 들어 키 저장소에 이미 존재하는 첫 번째 계정의 잔액을 확인하려면 다음을 수행하십시오.

```javascript
eth.getBalance(eth.accounts[0]);
```

트랜잭션을 보내려면(글로벌 계정 잠금 해제 없이):

```javascript
eth.sendTransaction({
  to: eth.accounts[0],
  to: eth.accounts[1],
  value: web3.toWei(0.5, 'ether')
});
```

콘솔을 시작할 때 --preload 플래그 를 전달하여 미리 작성된 Javascript 파일을 콘솔에 로드할 수도 있습니다 . 이는 복잡한 계약 개체를 설정하거나 자주 사용하는 기능을 로드하는 데 유용합니다.

```sh
geth console --preload "/my/scripts/folder/utils.js"
```

대화식 세션이 끝나면 exit 또는 CTRL-D를 입력하여 콘솔을 닫을 수 있습니다 .

계정과 관련된 상호 작용은 수동으로 또는 사용자 정의 규칙 세트를 작성하여 Clef에서 승인이 필요하다는 점을 기억하십시오.

### 비대화형 사용: 스크립트 모드 <a href="#non-interactive-use" id="non-interactive-use"></a>

geth attach 또는 geth console 에 --exec 및 JSON-RPC-API 엔드포인트를 전달하여 JavaScript 코드를 비대화식으로 실행할 수도 있습니다 . 결과는 대화식 Javascript 콘솔이 아닌 터미널에 직접 표시됩니다.

예를 들어 키 저장소의 계정을 표시하려면 다음을 수행하십시오.

```sh
geth attach --exec eth.accounts
```

```sh
geth attach --exec eth.blockNumber
```

동일한 구문을 사용하여 http를 통해 원격 노드에서 더 복잡한 명령문이 포함된 로컬 스크립트 파일을 실행할 수 있습니다. 예를 들면 다음과 같습니다.

```sh
geth attach http://geth.example.org:8545 --exec 'loadScript("/tmp/checkbalances.js")'

geth attach http://geth.example.org:8545 --jspath "/tmp" --exec 'loadScript("checkbalances.js")'
```

\--jspath 플래그는 Javascript 스크립트의 라이브러리 디렉토리를 설정하는 데 사용됩니다 . 명시적으로 절대 경로를 정의하지 않는 loadScript() 에 전달된 모든 매개변수는 jspath 디렉토리 에 상대적으로 해석됩니다 .
