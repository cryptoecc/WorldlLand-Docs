# Account Mangement

## Account security



Account security is very important in blockchain networks. You should make sure that your account's private key and password are inaccessible to anyone but yourself. If someone else obtains your account's private key and password, they can control all assets associated with your account. You should safely back up your account. If you lose your key file or password, your account assets are inaccessible and permanently lost.

ETH-ECC's node client has an internal account management tool. However, for better security, an off-client account management tool is desirable. Clef, an external account management tool supported by ETH-ECC, can be run separately from the client and operates on independent hardware. Clef requires manual review of account-related actions by the owner, and is more secure than traditional account management because signing is done inside Clef.

{% hint style="warning" %}
**Keep your account safe and backed up!**
{% endhint %}



### Account Management with Clef

#### **Clef init**

계정을 생성하기 전에 먼저 Clef를 초기화해야 합니다. Clef 의 경로를 결정하고 저장소 경로를 clef init 명령어로 전달하십시오.

```sh
$ ./clef init /CLEF_DIR/clefdata
```



{% hint style="info" %}
생성된마스터 시드를 기억하고 안전하게 보관하십시오.  마스터C시드를l통해ef가 관리하는 계정에 액세스할 수 있습니다.
{% endhint %}

### ETH-ECC 와 Clef 연결 <a href="#connecting-geth-and-clef" id="connecting-geth-and-clef"></a>

Clef 와 ETH-ECC가 서로 통신하기 위해서는 Cleft는 네트워크의 체인 아이디와 노드의 키 저장소의 위치를 알아야 합니다. 일반적으로 키 저장소는 노드 데이터 디렉토리 내부에 위치합니다.



Curl을 사용하여 Clef와의 통신을 활성화하려면 기본적으로 localhost:8550 에서 HTTP 서버를 시작하는 --http를 전달할 수 있습니다 .&#x20;

서울 메인넷에  연결하는 ETH-ECC 노드용으로 구성된 Clef를 시작하려면 다음 명령어를 실행하십시오.

```sh
$ ./clef -chainid 103 -keystore ~/ETH-ECC_DIR/keystore -configdir /CLEF_DIR/clef --http
```

Clef는 "확인"을 클릭하라는 면책 조항과 프롬프트로 시작하여 터미널에서 실행을 시작합니다.

```
WARNING!

Clef is an account management tool. It may, like any software, contain bugs.

Please take care to
- backup your keystore files,
- verify that the keystore(s) can be opened with your password.

Clef is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY;
without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR
PURPOSE. See the GNU General Public License for more details.

Enter 'ok' to proceed:
>
```

ETH-ECC는 별도의 터미널에서 시작할 수 있습니다. Clef에 연결하려면 데이터 디렉토리가 Clef에 제공된 경로와 일치하는지 확인하고 Clef IPC 파일의 위치를 ​​전달합니다. Clef는 이 파일을 -configdir 플래그에 제공된 경로에 저장합니다.&#x20;

```sh
./worldland -signer=/CLEF_DIR/clef/clef.ipc
```

### &#x20;<a href="#interacting-with-clef" id="interacting-with-clef"></a>

### 클레프와 상호 작용 <a href="#interacting-with-clef" id="interacting-with-clef"></a>

Clef와의 상호 작용에는 두 가지 모드가 있습니다. 하나는 Clef의 외부 API에 정의된 JSON-RPC 데이터와 함께 HTTP 또는 IPC로 요청을 전달하여 달성되는 직접적인 상호 작용입니다. 이것은 계정 생성 및 나열 또는 오프라인 데이터 서명과 같이 Geth가 필요하지 않은 작업을 Clef에서 수행하는 방법입니다. 다른 방법은 Geth를 이용하는 것입니다. Geth가 Clef를 외부 서명자로 시작했기 때문에 계정 데이터를 다루는 Geth에 대한 요청은 승인을 위해 Clef를 통해 라우팅됩니다. 기본적으로 사용자는 프롬프트가 표시될 때 Clef 콘솔에 y 또는 n을 입력하여 상호 작용을 수동으로 승인하거나 거부하지만 사용자 지정 규칙을 만들어 일반 작업을 자동화할 수도 있습니다.

#### 계정 생성 <a href="#creating-accounts" id="creating-accounts"></a>

Clef의 account new 방법을 사용하여 새 계정을 만들 수 있습니다 . 이렇게 하면 새 키 쌍이 생성되고 지정된 키 저장소 디렉토리에 추가됩니다.

```sh
clef newaccount --keystore sepolia-data/keystore
```

Clef는 터미널에서 새 암호를 요청합니다.

원시 JSON 요청을 사용하여 동일한 결과를 얻을 수 있습니다(이 예에서는 curl을 사용하여 Clef의 노출된 HTTP 포트로 요청을 보냅니다).

```sh
curl -X POST --data '{"id": 0, "jsonrpc": "2.0", "method": "account_new", "params": []}' http://localhost:8550 -H "Content-Type: application/json"
```

Clef가 수동 승인을 기다리고 있기 때문에 콘솔이 중단됩니다. Clef 터미널로 전환하고 작업을 승인합니다. Clef는 계정 암호를 묻는 메시지를 표시한 다음 터미널 로그에서 계정 생성을 확인합니다. go-ethereum/sepolia-data 의 키 저장소에 새 키 파일이 추가되었습니다 . 결과 필드 에 새 계정 주소가 포함된 JSON 응답이 요청이 시작된 터미널로 반환됩니다 .

`{"jsonrpc": "2.0", "id": 0, "result": "0x168bc315a2ee09042d83d7c5811b533620531f67"}`

계정 암호는 검색하거나 재설정할 수 없으므로 안전하고 확실하게 백업하는 것이 중요합니다.



새로 생성된 키 파일은 \<datadir>/keystore/ 에서 볼 수 있습니다 . 파일 이름 지정 형식은 UTC--<날짜>--<주소> 입니다 . 여기서 날짜 는 [UTC 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 에 따라 시간 오프셋이 0이고 소수점 이하 8자리까지 정확한 초를 사용하여 형식이 지정된 키 생성 날짜 및 시간입니다 . address 는 선행 0x 없이 계정 주소를 구성하는 40개의 16진수 문자입니다 . 예를 들면 다음과 같습니다.

UTC--2022-05-19T12-34-36.47413510Z--0b85e5a13e118466159b1e1b6a4234e5f9f784bb

다음과 같이 clef importraw를 사용하여 원시 개인 키(16진수 문자열)를 가져와서 계정을 만들 수도 있습니다 .

```sh
clef importraw <hexkey>
```

터미널은 다음 메시지로 응답하여 계정이 성공적으로 생성되었음을 나타냅니다.

`## Info Key imported: Address 0x9160DC9105f7De5dC5E7f3d97ef11DA47269BdA6 Keystore file: /home/user/.ethereum/keystore/UTC--2022-10-28T12-03-13.976383602Z--9160dc9105f7de5dc5e7f3d97ef11da47269bda6 The key is now encrypted; losing the password will result in permanently losing access to the key and all associated funds! Make sure to backup keystore and passwords in a safe location.`

#### 계정 나열 <a href="#listing-accounts" id="listing-accounts"></a>

다음과 같이 간단한 CLI 명령을 사용하여 키 저장소의 계정을 터미널에 나열할 수 있습니다.

```sh
clef list-accounts --keystore <path-to-keystore>
```

또는 다음과 같이 POST 요청에서 account\_list를 사용합니다.

```sh
curl -X POST --data '{"id": 0, "jsonrpc": "2.0", "method": "account_list", "params": []}' http://localhost:8550 -H "Content-Type: application/json"
```

그러면 결과 필드 의 배열에 계정 주소가 있는 JSON 개체가 반환됩니다 .

`{"jsonrpc": "2.0", "id": 0, "result": ["0x168bc315a2ee09042d83d7c5811b533620531f67", "0x0b85e5a13e118466159b1e1b6a4234e5f9f784bb"]}`

계정이 나열될 때의 순서는 사전식이지만 파일 이름의 타임스탬프로 인해 생성 시간을 기준으로 사실상 연대순입니다. Ethereum 노드 간에 전체 키 저장소 디렉터리 또는 개별 키 파일을 전송하는 것이 안전합니다. 이는 다른 노드에서 계정을 추가할 때 키 저장소의 계정 순서가 변경될 수 있기 때문에 중요합니다. 따라서 스크립트 또는 코드 스니펫의 계정 인덱스에 의존하지 않는 것이 중요합니다.

eth.accounts 를 사용하여 Javascript 콘솔에 계정을 나열할 수도 있으며 승인을 위해 Clef에게 맡깁니다.

개별 계정뿐만 아니라 Clef가 관리하는 모든 지갑을 나열할 수 있습니다(지갑 상태와 포함된 모든 계정의 주소 및 URL도 인쇄합니다. 이것은 list- wallets CLI 명령을 사용합니다.

```sh
clef list-wallets --keystore <path-to-keystore>
```

다음을 반환합니다.

`- Wallet 0 at keystore:///home/user/Code/go-ethereum/testdata/keystore/UTC--2022-11-01T17-05-01.517877299Z--4f4094babd1a8c433e0f52a6ee3b6ff32dee6a9c (Locked ) - Account 0: 0x4f4094BaBd1A8c433e0f52A6ee3B6ff32dEe6a9c (keystore:///home/user/go-ethereum/testdata/keystore/UTC--2022-11-01T17-05-01.517877299Z--4f4094babd1a8c433e0f52a6ee3b6ff32dee6a9c) - Wallet 1 at keystore:///home/user/go-ethereum/testdata/keystore/UTC--2022-11-01T17-05-11.100536003Z--8ef15919f852a8034688a71d8b57ab0187364009 (Locked ) - Account 0: 0x8Ef15919F852A8034688a71d8b57Ab0187364009 (keystore:///home/user/go-ethereum/testdata/keystore/UTC--2022-11-01T17-05-11.100536003Z--8ef15919f852a8034688a71d8b57ab0187364009)`

#### 키 파일 가져오기 <a href="#importing-a-keyfile" id="importing-a-keyfile"></a>

기존 개인 키를 가져와서 계정을 생성하는 것도 가능합니다. 예를 들어, 사용자는 브라우저 지갑을 사용하여 생성한 주소에 이미 약간의 이더를 가지고 있을 수 있으며 이제 새로운 Geth 노드를 사용하여 자금과 상호 작용하기를 원할 수 있습니다. 이 경우 브라우저 지갑에서 개인 키를 내보내고 Geth로 가져올 수 있습니다. Clef를 사용하여 이 작업을 수행할 수 있지만 현재 메서드는 외부에 노출되지 않으며 UI 구현이 필요합니다. 예제로 사용하거나 기본 콘솔 UI를 사용하여 수행할 수 있는 Python UI가 Geth GitHub에 있습니다. 그러나 현재 개인 키에서 계정을 가져오는 가장 간단한 방법은 Geth의 계정 가져오기를 사용하는 것입니다 .

Geth는 개인 키가 16진수로 인코딩된 암호화되지 않은 정규 타원 곡선 바이트(예: 선행 0x가 없는 일반 텍스트 키)로 개인 키를 포함하는 파일로 저장되도록 개인 키를 요구합니다. 그런 다음 새 계정은 사용자가 요청 시 제공하는 암호로 보호되는 암호화된 형식으로 저장됩니다. 항상 그렇듯이 이 암호는 안전하고 안전하게 백업해야 합니다. 암호를 잊은 경우 검색하거나 재설정할 방법이 없습니다!

```sh
$ geth account import --datadir /some-dir ./keyfile
```

가져오기 성공을 나타내는 다음 정보가 터미널에 표시됩니다.

`Please enter a passphrase now. Passphrase: Repeat Passphrase: Address: {7f444580bfef4b9bc7e14eb7fb2a029336b07c9d}`

키 파일을 한 키 저장소에서 다른 키 저장소로 직접 복사할 수 있기 때문에 Geth 인스턴스 간에 계정을 전송하는 사용자에게는 이 가져오기/내보내기 프로세스가 **필요하지 않습니다 .**

계정 암호를 .txt 파일에 일반 텍스트로 저장하고 시작 시 --password 플래그 와 함께 해당 경로를 전달하여 비대화형 모드에서 계정을 가져올 수도 있습니다 .

```sh
geth account import --password path/password.txt path/keyfile
```

이 경우 의도된 사용자 외에는 암호 파일을 읽을 수 없도록 하는 것이 중요합니다. 이것은 파일 권한을 변경하여 달성할 수 있습니다. Linux에서 다음 명령은 현재 사용자만 액세스할 수 있도록 파일 권한을 업데이트합니다.

```sh
chmod 700 /path/to/password
cat > /path/to/password
<type password here>
```

#### &#x20;<a href="#import-presale-wallet" id="import-presale-wallet"></a>

### 계정 업데이트 <a href="#updating-accounts" id="updating-accounts"></a>

Clef는 기존 키 저장소 파일의 암호를 설정하고 제거하는 데 사용할 수 있습니다. 새 암호를 설정하려면 계정 주소를 setpw 에 전달합니다 .

```sh
clef setpw a94f5374fce5edbc8e2a8697c15331677e6ebf0b
```

이렇게 하면 Clef가 새 비밀번호를 두 번 입력한 다음 Clef 마스터 비밀번호를 입력하여 키 파일을 해독합니다.

Geth의 계정 업데이트 하위 명령을 사용하여 계정 비밀번호를 업데이트할 수도 있습니다.

```sh
geth account update a94f5374fce5edbc8e2a8697c15331677e6ebf0b
```

또는 비대화형 모드에서 암호화되지 않은 일반 텍스트의 계정 암호를 포함하는 암호 파일의 경로를 --password 플래그와 함께 전달할 수 있습니다.

```sh
geth account update a94f5374fce5edbc8e2a8697c15331677e6ebf0b --password path/password.txt
```

geth account update를 사용하여 계정을 업데이트하면 원본 파일이 새 파일로 대체됩니다. 즉, 업데이트된 원본 파일은 더 이상 사용할 수 없습니다. 키 파일을 최신 형식으로 업데이트하는 데 사용할 수 있습니다.

### 계정 잠금 해제 <a href="#unlocking-accounts" id="unlocking-accounts"></a>

Clef를 사용하면 무차별적인 계정 잠금 해제가 더 이상 기능이 아닙니다. 대신 규칙 집합에 인코딩된 특정 시나리오를 준수하지 않는 한 사용자가 수동으로 명시적으로 승인할 때까지 Clef 잠금 해제가 잠깁니다. 규칙 세트를 만드는 방법에 대한 지침은 Clef 문서를 참조하세요.

#### 업무 <a href="#transactions" id="transactions"></a>

트랜잭션은 Geth에 대한 원시 JSON 요청을 사용하거나 Javascript 콘솔에서 web3js를 사용하여 보낼 수 있습니다 . 어느 쪽이든, 서명자 역할을 하는 Clef와 함께 트랜잭션은 Clef에서 승인될 때까지 전송되지 않습니다. 다음 코드 스니펫은 Javascript 콘솔을 사용하여 키 저장소의 두 계정 간에 트랜잭션을 보내는 방법을 보여줍니다.

```sh
var tx = {from: eth.accounts[1], to: eth.accounts[2], value: web3.toWei(5, "ether")}

# this will hang until approval is given in the Clef console
eth.sendTransaction(tx)
```

### 요약 <a href="#summary" id="summary"></a>

이 페이지에서는 Clef와 Geth의 계정 관리 도구를 사용하여 계정을 관리하는 방법을 설명했습니다. 계정은 비밀번호로 암호화되어 저장됩니다. 계정 비밀번호와 키 저장소 디렉토리를 안전하게 백업하는 것이 중요합니다.
