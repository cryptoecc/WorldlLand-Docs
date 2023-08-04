# Security

## Network security

Since the Worldland blockchain network is a peer-to-peer network, it must be able to communicate with all nodes. The default port settings of ETH-ECC are as follows.

| Communication | Port  |
| ------------- | ----- |
| P2P           | 30303 |
| HTTP-RPC      | 8545  |
| WS-RPC        | 8546  |

**P2P 네트워크**는 기본적으로 설정되어 있으며, **HTTP** 와 **웹소켓(WS)**는 명령어를 활성화 하지 않으면, 기본적으로 비활성화입니다.



**월드랜드 네트워크 노드**의 네트워크 방화벽 설정은 다음과 같습니다.&#x20;

* TCP 30303 또는 P2P 통신을 위해 정의된 사용자 지정 포트 에서 트래픽을 허용합니다 . 이렇게 하면 노드가 피어에 연결할 수 있습니다.
* UDP 30303 또는 P2P 통신을 위해 정의된 사용자 지정 포트 에서 트래픽을 허용합니다 . 이를 통해 노드 검색이 가능합니다.

**JSON-RPC 서버를 활성화 한다면, 아래 설정을 포함하십시오.**

{% hint style="info" %}
When enabling **RPC servers** on Worldland nodes, security must be taken into account. When a node allows external access, an attacker with an unlocked account can easily transfer the ether stored in the wallet.



Please refer to the link below:

[https://ethereum.stackexchange.com/questions/3887/how-to-reduce-the-chances-of-your-ethereum-wallet-getting-hacked](https://ethereum.stackexchange.com/questions/3887/how-to-reduce-the-chances-of-your-ethereum-wallet-getting-hacked)
{% endhint %}

* 8545 에 대한 모든 트래픽 또는 노드에 대한 JSON-RPC 요청에 대해 정의된 모든 사용자 정의 포트(명시적으로 정의된 신뢰할 수 있는 시스템의 트래픽 제외)를 차단합니다.
* 8546 에 대한 모든 트래픽 또는 노드에 대한 JSON-RPC 요청에 대해 정의된 모든 사용자 정의 포트(명시적으로 정의된 신뢰할 수 있는 시스템의 트래픽 제외)를 차단합니다.



**P2P 포트**를 변경하고 싶다면, 명령줄 옵션의 `-port 옵션들을 참고하십시오.`

```
    --discovery.port value         (default: 30303)
          Use a custom UDP port for P2P discovery
    --port value                   (default: 30303)
          Network listening port
    --http.port value              (default: 8545)
          HTTP-RPC server listening port
    --ws.port value                (default: 8546)
          WS-RPC server listening port
          
```

### &#x20;<a href="#account-security" id="account-security"></a>

## Account security







계정 보안은 개인 키와 계정 암호를 백업하고 적이 액세스할 수 없도록 유지하는 것입니다. 이것은 사용자가 책임지는 것입니다. Geth는 계정 암호를 사용하여 잠금 해제된 키에 대해 암호화된 저장소를 제공합니다. 키 파일이나 암호를 분실하면 계정에 액세스할 수 없으며 자금은 사실상 영원히 손실됩니다. 암호화되지 않은 키에 대한 액세스 권한을 적이 획득한 경우 계정과 관련된 모든 자금을 제어할 수 있습니다.

Geth에는 계정 관리 도구가 내장되어 있습니다. 그러나 Clef는 외부 계정 관리 및 서명 도구로 권장됩니다. Geth에서 분리하여 실행할 수 있으며 VM 또는 보안 USB 드라이브와 같은 전용 보안 외부 하드웨어에서도 실행할 수 있습니다. 미리 정의된 특정 규칙이 구현된 경우를 제외하고 민감한 데이터를 다루는 모든 작업을 사용자가 수동으로 검토해야 하므로 이는 모범 사례로 간주됩니다. 서명은 노드에 대한 키 액세스를 제공하는 대신 Clef에 대해 로컬로 수행됩니다. Geth의 기본 제공 관리 도구는 가까운 시일 내에 더 이상 사용되지 않을 예정입니다.

**키 저장소와 암호를 안전하고 확실하게 백업하십시오!**
