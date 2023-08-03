# Eth

eth 네임스페이스 의 API 메서드에 대한 설명서는 [ethereum.org](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth\_protocolversion) 에서 찾을 수 있습니다 . Geth는 아래에 정의된 표준 "eth" JSON-RPC 네임스페이스에 대한 여러 확장을 제공합니다.

#### eth\_subscribe, eth\_unsubscribe <a href="#eth-subscribe-unsubscribe" id="eth-subscribe-unsubscribe"></a>

이러한 방법은 구독을 통한 실시간 이벤트에 사용됩니다. 자세한 내용은 [구독 설명서를](https://geth.ethereum.org/docs/interacting-with-geth/rpc/pubsub) 참조하십시오 .

#### eth\_call <a href="#eth-call" id="eth-call"></a>

블록체인에 트랜잭션을 생성하지 않고 즉시 새로운 메시지 호출을 실행합니다. eth\_call 메서드를 사용하여 내부 계약 상태를 쿼리하거나 계약에 코딩된 유효성 검사 를 실행하거나 트랜잭션을 실시간으로 실행하지 않고 트랜잭션의 영향을 테스트하는 데 사용할 수 있습니다.

**매개변수**

이 메서드는 3개의 매개 변수를 사용합니다. 읽기 전용 모드에서 실행할 서명되지 않은 트랜잭션 개체입니다. 호출을 실행할 블록 번호; 수정된 체인 상태에 대해 호출을 실행할 수 있도록 하는 선택적 상태 재정의 설정입니다.

**1. 객체 - 트랜잭션 호출 객체**

트랜잭션 _호출 개체는_ 필수입니다. [자세한 내용은 여기를](https://geth.ethereum.org/docs/interacting-with-geth/rpc/objects) 참조하십시오 .

**2. 수량 | 태그 - 블록 번호 또는 최신 또는 보류 중인 문자열**

블록 _번호_ 는 필수이며 지정된 트랜잭션이 실행되어야 하는 컨텍스트(상태)를 정의합니다. 재구성된 블록에 대해 호출을 실행할 수 없습니다. 또는 128보다 오래된 블록(노드가 아카이브 노드가 아닌 경우).

**3. 개체 - 상태 재정의 설정**

상태 _재정의 세트_ 는 선택적인 주소 대 상태 매핑이며 각 항목은 호출을 실행하기 전에 일시적으로 재정의할 일부 상태를 지정합니다. 각 주소는 다음을 포함하는 개체에 매핑됩니다.

| 필드        | 유형   | 바이트 | 선택 과목 | 설명                                                   |
| --------- | ---- | --- | ----- | ---------------------------------------------------- |
| 균형        | 수량   | <32 | 예     | 호출을 실행하기 전에 계정에 설정할 가짜 잔액.                           |
| 목하        | 수량   | <8  | 예     | 호출을 실행하기 전에 계정에 설정할 가짜 논스.                           |
| 암호        | 바이너리 | 어느  | 예     | 호출을 실행하기 전에 계정에 삽입할 가짜 EVM 바이트코드.                    |
| 상태        | 물체   | 어느  | 예     | 호출을 실행하기 전에 계정 스토리지의 **모든** 슬롯을 재정의하는 가짜 키-값 매핑입니다 . |
| stateDiff | 물체   | 어느  | 예     | 호출을 실행하기 전에 계정 저장소의 **개별** 슬롯을 재정의하는 가짜 키-값 매핑입니다 .  |

_상태 재정의 세트_ 의 목표는 여러 가지입니다.

* DApp에서 체인에 배포하는 데 필요한 계약 코드의 양을 줄이는 데 사용할 수 있습니다. 단순히 내부 상태를 반환하거나 미리 정의된 유효성 검사를 수행하는 코드는 오프체인으로 유지하고 필요에 따라 노드에 공급할 수 있습니다.
* 사용자 지정 메서드로 체인에 배포된 코드를 확장하고 이를 호출하여 스마트 계약 분석에 사용할 수 있습니다. 이렇게 하면 사용자 지정 코드를 실행하기 위해 샌드박스에서 전체 상태를 다운로드하고 재구성할 필요가 없습니다.
* 일부 코드 또는 상태를 선택적으로 재정의하고 실행이 어떻게 변경되는지 확인하여 이미 배포된 대규모 계약 제품군에서 스마트 계약을 디버깅하는 데 사용할 수 있습니다. 특수 도구가 필요할 것입니다.

예:

```json
{
  "0xd9c9cd5f6779558b6e0ed4e6acf6b1947e7fa1f3": {
    "balance": "0xde0b6b3a7640000"
  },
  "0xebe8efa441b9302a0d7eaecc277c09d20d684540": {
    "code": "0x...",
    "state": {
      ""
    }
  }
}
```

**반환 값**

이 메서드는 실행된 계약 호출의 반환 값으로 구성된 단일 바이너리를 반환합니다.

**간단한 예**

**이 예제는 현재 더 이상 사용되지 않는 Rinkeby 네트워크를 사용합니다.**

localhost( geth --rinkeby --http ) 에 RPC가 노출된 동기화된 Rinkeby 노드를 사용하여 [CheckpointOracle](https://rinkeby.etherscan.io/address/0xebe8efa441b9302a0d7eaecc277c09d20d684540) 에 대해 호출하여 관리자 목록을 검색할 수 있습니다.

```sh
$ curl --data '{"method":"eth_call","params":[{"to":"0xebe8efa441b9302a0d7eaecc277c09d20d684540","data":"0x45848dfc"},"latest"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545
```

결과는 Ethereum ABI로 인코딩된 계정 목록입니다.

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "result": "0x00000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000004000000000000000000000000d9c9cd5f6779558b6e0ed4e6acf6b1947e7fa1f300000000000000000000000078d1ad571a1a09d60d9bbf25894b44e4c8859595000000000000000000000000286834935f4a8cfb4ff4c77d5770c2775ae2b0e7000000000000000000000000b86e2b0ab5a4b1373e40c51a7c712c70ba2f9f8e"
}
```

완전성을 위해 응답을 디코딩하면 다음과 같습니다.

```sh
0xd9c9cd5f6779558b6e0ed4e6acf6b1947e7fa1f3,
0x78d1ad571a1a09d60d9bbf25894b44e4c8859595,
0x286834935f4a8cfb4ff4c77d5770c2775ae2b0e7,
0xb86e2b0ab5a4b1373e40c51a7c712c70ba2f9f8e
```

**재정의 예**

위의 _간단한 예는_ 온체인 스마트 계약에 의해 이미 노출된 메소드를 호출하는 방법을 보여줍니다. 노출되지 않은 일부 데이터에 액세스하려면 어떻게 해야 합니까?

동일한 필드를 유지하지만(동일한 스토리지 레이아웃을 유지하기 위해) 다른 메소드 세트를 포함하는 [원래](https://github.com/ethereum/go-ethereum/blob/master/contracts/checkpointoracle/contract/oracle.sol) 체크포인트 오라클 계약을 제거할 수 있습니다 .

```javascript
pragma solidity ^0.5.10;

contract CheckpointOracle {
    mapping(address => bool) admins;
    address[] adminList;
    uint64 sectionIndex;
    uint height;
    bytes32 hash;
    uint sectionSize;
    uint processConfirms;
    uint threshold;

    function VotingThreshold() public view returns (uint) {
        return threshold;
    }
}
```

localhost( geth --rinkeby --http ) 에 노출된 RPC가 있는 동기화된 Rinkeby 노드를 사용하여 라이브 [Checkpoint Oracle](https://rinkeby.etherscan.io/address/0xebe8efa441b9302a0d7eaecc277c09d20d684540) 에 대해 호출할 수 있지만 투표 임계값 필드에 대한 접근자가 있는 자체 버전으로 바이트 코드를 재정의할 수 있습니다.

```sh
$ curl --data '{"method":"eth_call","params":[{"to":"0xebe8efa441b9302a0d7eaecc277c09d20d684540","data":"0x0be5b6ba"}, "latest", {"0xebe8efa441b9302a0d7eaecc277c09d20d684540": {"code":"0x6080604052348015600f57600080fd5b506004361060285760003560e01c80630be5b6ba14602d575b600080fd5b60336045565b60408051918252519081900360200190f35b6007549056fea265627a7a723058206f26bd0433456354d8d1228d8fe524678a8aeeb0594851395bdbd35efc2a65f164736f6c634300050a0032"}}],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545
```

결과는 Ethereum ABI로 인코딩된 임계값입니다.

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "result": "0x0000000000000000000000000000000000000000000000000000000000000002"
}
```

완전성을 위해 디코딩된 응답은 다음과 같습니다. 2 .

#### eth\_createAccessList <a href="#eth-createaccesslist" id="eth-createaccesslist"></a>

이 메소드는 주어진 트랜잭션을 기반으로 [EIP2930](https://eips.ethereum.org/EIPS/eip-2930) 유형 accessList를 생성합니다 . accessList 에는 발신자 계정과 사전 컴파일을 제외하고 트랜잭션에서 읽고 쓴 모든 저장소 슬롯과 주소가 포함됩니다. 이 메서드는 eth\_call 과 동일한 트랜잭션 호출 [개체](https://geth.ethereum.org/docs/interacting-with-geth/rpc/objects#transaction-call-object) 및 blockNumberOrTag 개체를 사용합니다 . accessList는 가스 비용 증가로 인해 액세스할 수 없게 된 계약을 해제하는 데 사용할 수 있습니다.

**매개변수**

| 필드               | 유형 | 설명                         |
| ---------------- | -- | -------------------------- |
| 거래               | 물체 | 트랜잭션콜 객체                   |
| blockNumberOrTag | 물체 | 선택 사항, 블록 번호 또는 최신 또는 보류 중 |

**용법**

`curl --data '{"method":"eth_createAccessList","params":[{"from": "0x8cd02c6cbd8375b39b06577f8d50c51d86e8d5cd", "data": "0x608060806080608155"}, "pending"],"id":1,"jsonrpc":"2.0"}' -H "Content-Type: application/json" -X POST localhost:8545`

**응답**

eth\_createAccessList 메서드는 트랜잭션에서 사용하는 주소 및 스토리지 키 목록과 액세스 목록이 추가될 때 소비되는 가스를 반환합니다.

즉, 해당 트랜잭션에서 사용할 주소 및 스토리지 키 목록과 액세스 목록이 포함된 경우 소비되는 가스를 제공합니다. eth\_estimateGas 와 마찬가지로 추정치입니다. 트랜잭션이 실제로 채굴될 때 목록이 변경될 수 있습니다. 트랜잭션에 accessList를 추가해도 액세스 목록이 없는 트랜잭션에 비해 가스 사용량이 낮아지는 것은 아닙니다.

예:

```json
{
  "accessList": [
    {
      "address": "0xa02457e5dfd32bda5fc7e1f1b008aa5979568150",
      "storageKeys": [
        "0x0000000000000000000000000000000000000000000000000000000000000081",
      ]
    }
  ]
  "gasUsed": "0x125f8"
}
```

#### eth\_getHeaderByNumber <a href="#ethgetheaderbynumber" id="ethgetheaderbynumber"></a>

블록 헤더를 반환합니다.

**매개변수**

| 필드    | 유형 | 설명    |
| ----- | -- | ----- |
| 블록 번호 | 수량 | 블록 번호 |

**용법**

`curl localhost:8545 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_getHeaderByNumber","params":["0x10823a8"],"id":0}'`

**응답**

```json
{
  baseFeePerGas: "0x6c3f71624",
  difficulty: "0x0",
  extraData: "0x496c6c756d696e61746520446d6f63726174697a6520447374726962757465",
  gasLimit: "0x1c9c380",
  gasUsed: "0x1312759",
  hash: "0x4574b6f248bf3295f76ae797454f4ec21c8ef5b53c0f7fee8534b65623d9360a",
  logsBloom: "0x04a13010898372c9ca19007ccd04eed1f707098f04123de47da9d0b67ce1a60ab8ea324cd8291c36a8ca5a520893d1552711012dba82ad817332008d90ac788047c0fcd2d1200cb82bd1690b32b6d7ab8ab28a86b1f7095a19b59104d062882093746d041b510537a4d0015518c1583de073045981792d0030aa5cd5089a0a700160f74b0b250a9e30ea90596fdf851732815da30d800ace471e2768e09bc0d45e79f97238136523021a4bd52d45a5e184c8c810a9c22afa8670b6bab0eb2636ea1981120a400040829021a3e96cbe0262d8a6ba06006b37249117230968eecc0c16a7ae4090e888673f1101a27159d5cd12a190f5aa85cb524dbc72f5d4ed14",
  miner: "0xdafea492d9c6733ae3d56b7ed1adb60692c98bc5",
  mixHash: "0xec33ce424110ddd8f7e7db1cbc1261a63e44dacd158b4e801566cd6d5849295b",
  nonce: "0x0000000000000000",
  number: "0x10823a8",
  parentHash: "0x956846b5012b1df4f4c928b85db2f6456b2faed2c0ca136e89c928a87ceec69c",
  receiptsRoot: "0x89b73c221ca0d721f8805edbecbf55524b0556dc5111680bac1c4dd02a286457",
  sha3Uncles: "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
  size: "0x25e",
  stateRoot: "0xe38ef58ddfbf00b03f7bd431fca306e5fcaecc138f4208501d2588657a65a0f3",
  timestamp: "0x646a982b",
  totalDifficulty: "0xc70d815d562d3cfa955",
  transactionsRoot: "0xe44699ea734cee851a852db4d257617c8369b8a7e68bd54b6de829377234017b",
  withdrawalsRoot: "0x917f5a8e4d652233a80b0973ff20bde517ed2a6a93defe7e99c5263089453e17"
}
```

#### eth\_getHeaderByHash <a href="#ethgetheaderbyhash" id="ethgetheaderbyhash"></a>

블록 헤더를 반환합니다.

**매개변수**

| 필드   | 유형 | 설명    |
| ---- | -- | ----- |
| 블록해시 | 끈  | 블록 해시 |

**용법**

`curl localhost:8545 -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_getHeaderByHash","params":["0x4574b6f248bf3295f76ae797454f4ec21c8ef5b53c0f7fee8534b65623d9360a"],"id":0}'`

**응답**

```json
{
  baseFeePerGas: "0x6c3f71624",
  difficulty: "0x0",
  extraData: "0x496c6c756d696e61746520446d6f63726174697a6520447374726962757465",
  gasLimit: "0x1c9c380",
  gasUsed: "0x1312759",
  hash: "0x4574b6f248bf3295f76ae797454f4ec21c8ef5b53c0f7fee8534b65623d9360a",
  logsBloom: "0x04a13010898372c9ca19007ccd04eed1f707098f04123de47da9d0b67ce1a60ab8ea324cd8291c36a8ca5a520893d1552711012dba82ad817332008d90ac788047c0fcd2d1200cb82bd1690b32b6d7ab8ab28a86b1f7095a19b59104d062882093746d041b510537a4d0015518c1583de073045981792d0030aa5cd5089a0a700160f74b0b250a9e30ea90596fdf851732815da30d800ace471e2768e09bc0d45e79f97238136523021a4bd52d45a5e184c8c810a9c22afa8670b6bab0eb2636ea1981120a400040829021a3e96cbe0262d8a6ba06006b37249117230968eecc0c16a7ae4090e888673f1101a27159d5cd12a190f5aa85cb524dbc72f5d4ed14",
  miner: "0xdafea492d9c6733ae3d56b7ed1adb60692c98bc5",
  mixHash: "0xec33ce424110ddd8f7e7db1cbc1261a63e44dacd158b4e801566cd6d5849295b",
  nonce: "0x0000000000000000",
  number: "0x10823a8",
  parentHash: "0x956846b5012b1df4f4c928b85db2f6456b2faed2c0ca136e89c928a87ceec69c",
  receiptsRoot: "0x89b73c221ca0d721f8805edbecbf55524b0556dc5111680bac1c4dd02a286457",
  sha3Uncles: "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
  size: "0x25e",
  stateRoot: "0xe38ef58ddfbf00b03f7bd431fca306e5fcaecc138f4208501d2588657a65a0f3",
  timestamp: "0x646a982b",
  totalDifficulty: "0xc70d815d562d3cfa955",
  transactionsRoot: "0xe44699ea734cee851a852db4d257617c8369b8a7e68bd54b6de829377234017b",
  withdrawalsRoot: "0x917f5a8e4d652233a80b0973ff20bde517ed2a6a93defe7e99c5263089453e17"
}
```
