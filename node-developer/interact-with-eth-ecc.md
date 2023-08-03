# Interact with ETH-ECC

블록체인과의 상호 작용을 위해 ETH-ECC는 JSON-RPC API를 제공합니다. [JSON-RPC는 ](https://ethereum.org/en/developers/docs/apis/json-rpc/)[JSON](https://www.json.org/json-en.html) 객체 형태로 ETH-ECC에 명령을 보내 특정 작업을 수행하는 방식입니다 . RPC는 "Remote Procedure Call"의 약자이며 ETH-ECC가 관리하는 위치 외부에서 이러한 JSON 인코딩 명령을 보내는 기능을 나타냅니다. Curl과 같은 도구를 사용하여 ETH-ECC의 노출된 http 포트를 통해 이러한 JSON 인코딩 지침을 직접 전송함으로써 ETH-ECC와 상호 작용할 수 있습니다. 그러나 이것은 다소 사용자에게 친숙하지 않고 특히 더 복잡한 명령의 경우 오류가 발생하기 쉽습니다. 이러한 이유로 JSON-RPC 위에 구축된 일련의 라이브러리가 Geth와 상호 작용하기 위한 보다 사용자 친화적인 인터페이스를 제공합니다. 가장 널리 사용되는 것 중 하나는 Web3.js입니다.

ETH-ECC는 Web3.js API를 노출하는 Javascript 콘솔을 제공합니다. 즉, 한 터미널에서 ETH-ECC를 실행하면 다른 터미널에서 Javascript 환경을 열어 사용자가 Web3.js를 사용하여 ETH-ECC와 상호 작용할 수 있습니다. Javascript 환경을 Geth에 연결하는 데 사용할 수 있는 세 가지 전송 프로토콜이 있습니다.

* IPC(Inter-Process Communication): 모든 API에 대한 무제한 액세스를 제공하지만 콘솔이 ETH-ECC 노드와 동일한 호스트에서 실행될 때만 작동합니다.
* HTTP: 기본적으로 eth , web3 및 net 메서드 네임스페이스에 대한 액세스를 제공합니다.
* Websocket: 기본적으로 eth , web3 및 net 메서드 네임스페이스에 대한 액세스를 제공합니다.

이 자습서에서는 HTTP 옵션을 사용합니다. ETH-ECC와 Clef를 실행하는 터미널은 둘 다 여전히 활성 상태여야 합니다. 새(세 번째) 터미널에서 다음 명령을 실행하여 콘솔을 시작하고 노출된 http 포트를 사용하여 ETH-ECC에 연결할 수 있습니다.
