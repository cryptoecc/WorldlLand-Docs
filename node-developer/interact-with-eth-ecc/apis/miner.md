# Miner

지분 증명으로 전환할 때 채굴이 꺼졌기 때문에 **이제 채굴기 API는 더 이상 사용** 되지 않습니다 . 노드의 마이닝 작업을 원격 제어하고 다양한 마이닝 관련 설정을 지정하기 위해 존재했습니다. 역사적인 관심을 위해 여기에 제공됩니다!

### miner\_getHashrate <a href="#miner-hashrate" id="miner-hashrate"></a>

H/s(초당 해시 작업)로 해시레이트를 가져옵니다.

| 고객  | 메서드 호출                                     |
| --- | ------------------------------------------ |
| 콘솔  | miner.getHashrate()                        |
| RPC | {"방법": "miner\_getHashrate", "매개 변수": \[]} |

### miner\_setExtra <a href="#miner-setextra" id="miner-setextra"></a>

광부가 차단할 때 광부가 포함할 수 있는 추가 데이터를 설정합니다. 이것은 32바이트로 제한됩니다.

| 고객  | 메서드 호출                                    |
| --- | ----------------------------------------- |
| 가다  | miner.setExtra(추가 문자열) (부울, 오류)           |
| 콘솔  | miner.setExtra(문자열)                       |
| RPC | {"방법": "miner\_setExtra", "매개변수": \[문자열]} |

### miner\_set가스 가격 <a href="#miner-setgasprice" id="miner-setgasprice"></a>

트랜잭션을 마이닝할 때 허용되는 최소 가스 가격을 설정합니다. 이 한도 미만의 모든 트랜잭션은 마이닝 프로세스에서 제외됩니다.

| 고객  | 메서드 호출                                       |
| --- | -------------------------------------------- |
| 가다  | miner.setGasPrice(숫자 \*rpc.HexNumber) 부울     |
| 콘솔  | miner.setGasPrice(숫자)                        |
| RPC | {"방법": "miner\_setGasPrice", "매개 변수": \[숫자]} |

### miner\_setRecommitInterval <a href="#miner-setrecommitinterval" id="miner-setrecommitinterval"></a>

광부 봉인 작업을 다시 커밋하는 간격을 업데이트합니다.

| 고객  | 메서드 호출                                               |
| --- | ---------------------------------------------------- |
| 콘솔  | miner.setRecommitInterval(간격 정수)                     |
| RPC | {"방법": "miner\_setRecommitInterval", "매개 변수": \[숫자]} |

### miner\_start <a href="#miner-start" id="miner-start"></a>

CPU 마이닝 프로세스를 시작합니다.

| 고객  | 메서드 호출                               |
| --- | ------------------------------------ |
| 가다  | miner.Start() 오류                     |
| 콘솔  | 광부.시작()                              |
| RPC | {"방법": "miner\_start", "매개 변수": \[]} |

### miner\_stop <a href="#miner-stop" id="miner-stop"></a>

CPU 마이닝 작업을 중지합니다.

| 고객  | 메서드 호출                              |
| --- | ----------------------------------- |
| 가다  | miner.Stop() 부울                     |
| 콘솔  | 광부.정지()                             |
| RPC | {"방법": "miner\_stop", "매개 변수": \[]} |

### miner\_setEtherbase <a href="#miner-setetherbase" id="miner-setetherbase"></a>

채굴 보상이 갈 이더베이스를 설정합니다.

| 고객  | 메서드 호출                                       |
| --- | -------------------------------------------- |
| 가다  | miner.SetEtherbase(common.Address) 부울        |
| 콘솔  | miner.setEtherbase(주소)                       |
| RPC | {"방법": "miner\_setEtherbase", "매개변수": \[주소]} |

### miner\_setGasLimit <a href="#miner-setgaslimit" id="miner-setgaslimit"></a>

광부가 채굴할 때 목표로 삼을 가스 한도를 설정합니다. 참고: EIP-1559가 활성화된 네트워크에서는 가스 목표(즉, 블록당 평균적으로 사용되는 유효 가스)의 두 배로 설정해야 합니다.

| 고객  | 메서드 호출                                       |
| --- | -------------------------------------------- |
| 가다  | miner.SetGasLimit(숫자 \*rpc.HexNumber) 부울     |
| 콘솔  | miner.SetGasLimit(숫자)                        |
| RPC | {"방법": "miner\_setGasLimit", "매개 변수": \[숫자]} |
