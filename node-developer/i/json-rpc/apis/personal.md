# Personal

The JSON-RPC API's personal namespace has historically been used to manage accounts and sign transactions and data over RPC. However, it has **now been deprecated** in favour of using [Clef](https://geth.ethereum.org/docs/tools/clef/introduction) as an external signer and account manager. One of the major changes is moving away from indiscriminate locking and unlocking of accounts and instead using Clef to explicitly approve or deny specific actions. The first section on this page shows the suggested replacement for each method in personal. The second section shows the deprecated methods for archival purposes.

### Method replacements <a href="#method-replacements" id="method-replacements"></a>

The following list shows each method from the personal namespace and the intended method in Clef that supercedes it.

#### personal\_listAccounts <a href="#personallistaccounts" id="personallistaccounts"></a>

personal\_listAccounts displays the addresses of all accounts in the keystore. It is identical to eth.accounts. Calling eth.accounts requires manual approval in Clef (unless a rule for it has been attested). There is also Clef's list-accounts command that can be called from the terminal.

Examples:

```sh
# eth_accounts using curl
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_accounts","params":[],"id":1}'
```

```javascript
// eth_accounts in Geth's JS console
eth.accounts;
```

```sh
# clef list-accounts in the terminal
clef list-accounts
```

#### personal\_deriveAccount <a href="#personalderiveaccount" id="personalderiveaccount"></a>

personal\_deriveAccount requests a hardware wallet to derive a new account, optionally pinning it for later use. This method is identical to clef\_deriveAccount. The Clef method is not externally exposed so it must be called via a UI.

#### personal.ecRecover <a href="#personalecrecover" id="personalecrecover"></a>

personal\_ecRecover returns the address for the account that was used to create a signature. An equivalent method, account\_ecRecover is available on the Clef external API.

Example call:

```sh
curl --data '{"id": 4, "jsonrpc": "2.0", "method": "account_ecRecover","params": ["0xaabbccdd",     "0x5b6693f153b48ec1c706ba4169960386dbaa6903e249cc79a8e6ddc434451d417e1e57327872c7f538beeb323c300afa9999a3d4a5de6caf3be0d5ef832b67ef1c"]}' -X POST localhost:8550
```

#### personal\_importRawKey <a href="#personalimportrawkey" id="personalimportrawkey"></a>

personal.importRawKey was used to create a new account in the keystore from a raw private key. Clef has an equivalent method that can be invoked in the terminal using:

```sh
clef importraw <private-key-as-hex-string>
```

#### personal\_listWallets <a href="#personallistwallets" id="personallistwallets"></a>

As opposed to listAccounts, this method lists full details, including usb path or keystore-file paths. The equivalent method is clef\_listWallets. This method can be called from the terminal using:

```sh
clef list-wallets
```

#### personal\_newAccount <a href="#personalnewaccount" id="personalnewaccount"></a>

personal\_newAccount was used to create a new accoutn and save it in the keystore. Clef has an equivalent method, account\_new. It can be accessed on the terminal using an http request or using a Clef command:

Example call (curl):

```sh
curl --data '{"id": 1, "jsonrpc": "2.0", "method": "account_new", "params": []}' -X POST localhost:8550
```

Example call (Clef command):

```sh
clef newaccount
```

Both require manual approval in Clef unless a custom ruleset is in place.

#### personal\_openWallet <a href="#personalopenwallet" id="personalopenwallet"></a>

personal\_OpenWallet initiates a hardware wallet opening procedure by establishing a USB connection and then attempting to authenticate via the provided passphrase. Note, the method may return an extra challenge requiring a second open (e.g. the Trezor PIN matrix challenge). personal\_openWallet is identical to clef\_openWallet. The Clef method is not externally eposed, meaning it must be called via a UI.

#### personal\_sendTransaction <a href="#personalsendtransaction" id="personalsendtransaction"></a>

personal\_sendTransaction ws used to sign and submit a transaction. This can be done using eth\_sendTransaction, requiring manual approval in Clef.

Example call (Javascript console):

```javascript
// this command requires 2x approval in Clef because it loads account data via eth.accounts[0]
// and eth.accounts[1]
var tx = { from: eth.accounts[0], to: eth.accounts[1], value: web3.toWei(0.1, 'ether') };

// then send the transaction
eth.sendTransaction(tx);
```

Example call (terminal)

```sh
curl --data '{"id":1, "jsonrpc":"2.0", "method":"eth_sendTransaction", "params":[{"from": "0xE70CAD05D0D54Ae3C9Fe5442f901E0433f9bd14B", "to":"0x4FDc03d09Ffca5Bba3138149E29D85C8A9E2Ac42", "gas":"21000","gasPrice":"20000000000", "nonce":"94"}]}' -H "Content-Type: application/json" -X POST localhost:8545
```

#### personal\_sign <a href="#personalsign" id="personalsign"></a>

The sign method calculates an Ethereum specific signature with sign(keccak256("\x19Ethereum Signed Message:\n" + len(message) + message)). Adding a prefix to the message makes the calculated signature recognisable as an Ethereum specific signature. This prevents misuse where a malicious DApp can sign arbitrary data (e.g. transaction) and use the signature to impersonate the victim.

personal.sign is equivalent to Clef's account\_signData. It returns the calculated signature.

Example call:

```sh
curl --data {"id": 3, "jsonrpc": "2.0", "method": "account_signData", "params": ["data/plain", "0x1923f626bb8dc025849e00f99c25fe2b2f7fb0db","0xaabbccdd"]} -X POST localhost:8550
```

Clef also has account\_signTypedData that signs data structured according to [EIP-712](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-712.md) and returns the signature.

Example call (use the following as a template for \<data> in curl --data \<data> -X POST localhost:8550 -H "Content-Type: application/json")

```json
{
  "id": 68,
  "jsonrpc": "2.0",
  "method": "account_signTypedData",
  "params": [
    "0xcd2a3d9f938e13cd947ec05abc7fe734df8dd826",
    {
      "types": {
        "EIP712Domain": [
          {
            "name": "name",
            "type": "string"
          },
          {
            "name": "version",
            "type": "string"
          },
          {
            "name": "chainId",
            "type": "uint256"
          },
          {
            "name": "verifyingContract",
            "type": "address"
          }
        ],
        "Person": [
          {
            "name": "name",
            "type": "string"
          },
          {
            "name": "wallet",
            "type": "address"
          }
        ],
        "Mail": [
          {
            "name": "from",
            "type": "Person"
          },
          {
            "name": "to",
            "type": "Person"
          },
          {
            "name": "contents",
            "type": "string"
          }
        ]
      },
      "primaryType": "Mail",
      "domain": {
        "name": "Ether Mail",
        "version": "1",
        "chainId": 1,
        "verifyingContract": "0xCcCCccccCCCCcCCCCCCcCcCccCcCCCcCcccccccC"
      },
      "message": {
        "from": {
          "name": "Cow",
          "wallet": "0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826"
        },
        "to": {
          "name": "Bob",
          "wallet": "0xbBbBBBBbbBBBbbbBbbBbbbbBBbBbbbbBbBbbBBbB"
        },
        "contents": "Hello, Bob!"
      }
    }
  ]
}
```

#### personal\_signTransaction <a href="#personalsigntransaction" id="personalsigntransaction"></a>

personal\_signTransaction was used to create and sign a transaction from the given arguments. The transaction was returned in RLP-form, not broadcast to other nodes. The equivalent method is Clef's account\_signTransaction from the external API. The arguments are a transaction object ({"from": , "to": , "gas": , "maxPriorityFeePerGas": , "MaxFeePerGas": , "value": , "data": , "nonce": })) and an optional method signature that enables Clef to decode the calldata and show the user the methods, arguments and values being sent.

Example call (terminal):

```sh
curl --data '{"id": 2, "jsonrpc": "2.0", "method": "account_signTransaction", "params": [{"from": "0x1923f626bb8dc025849e00f99c25fe2b2f7fb0db", "gas": "0x55555","gasPrice": "0x1234", "input": "0xabcd", "nonce": "0x0", "to": "0x07a565b7ed7d7a678680a4c162885bedbb695fe0", "value": "0x1234"}]}' -X POST -H "Content-Type: application/json" localhost:8550
```

### Methods without replacements <a href="#methods-without-replacements" id="methods-without-replacements"></a>

Thjere are a few methods that were available in the personal namepsace that have been deprecated without replacements. These are:

#### personal\_unlockAccount <a href="#personalunlockaccount" id="personalunlockaccount"></a>

There is no need for a direct replacement for personal\_unlockAccount. Using Clef to manually approve actions or to attest custom rulesets is a much more secure way to interact with accounts without needing to indiscriminately unlock accounts.

#### personal\_lockAccount <a href="#personallockaccount" id="personallockaccount"></a>

There is no need for a direct replacement for personal\_lockAccount because account locking/unlocking is replaced by Clef's approve/deny logic. This is a more secure way to interact with accounts.

#### personal.unpair <a href="#personalunpair" id="personalunpair"></a>

Unpair deletes a pairing between some specific types of smartcard wallet and Geth. There is not yet an equivalent method in Clef.

#### personal\_initializeWallet <a href="#personalinitializewallet" id="personalinitializewallet"></a>

InitializeWallet is for initializing some specific types of smartcard wallet at a provided URL. There is not yet a corresponding method in Clef.

### Deprecated method documentation <a href="#deprecated-method-documentation" id="deprecated-method-documentation"></a>

The personal API managed private keys in the key store. It is now deprecated in favour of using [Clef](https://geth.ethereum.org/docs/tools/clef/introduction) for interacting with accounts. The following documentation should be treated as archive information and users should migrate to using Clef for account interactions.

#### personal\_deriveAccount <a href="#personal-deriveaccount" id="personal-deriveaccount"></a>

Requests a HD wallet to derive a new account, optionally pinning it for later reuse.

| CLIENT  | METHOD INVOCATION                                                        |
| ------- | ------------------------------------------------------------------------ |
| Console | personal.deriveAccount(url, path, pin)                                   |
| RPC     | {"method": "personal\_deriveAccount", "params": \[string, string, bool]} |

#### personal\_importRawKey <a href="#personal-importrawkey" id="personal-importrawkey"></a>

Imports the given unencrypted private key (hex string) into the key store, encrypting it with the passphrase.

Returns the address of the new account.

| CLIENT  | METHOD INVOCATION                                                 |
| ------- | ----------------------------------------------------------------- |
| Console | personal.importRawKey(keydata, passphrase)                        |
| RPC     | {"method": "personal\_importRawKey", "params": \[string, string]} |

#### personal\_initializeWallets <a href="#personal-intializewallets" id="personal-intializewallets"></a>

Initializes a new wallet at the provided URL by generating and returning a new private key.

| CLIENT  | METHOD INVOCATION                                             |
| ------- | ------------------------------------------------------------- |
| Console | personal.initializeWallet(url)                                |
| RPC     | {"method": "personal\_initializeWallet", "params": \[string]} |

#### personal\_listAccounts <a href="#personal-listaccounts" id="personal-listaccounts"></a>

Returns all the Ethereum account addresses of all keys in the key store.

| CLIENT  | METHOD INVOCATION                                   |
| ------- | --------------------------------------------------- |
| Console | personal.listAccounts                               |
| RPC     | {"method": "personal\_listAccounts", "params": \[]} |

**Example**

```javascript
> personal.listAccounts
["0x5e97870f263700f46aa00d967821199b9bc5a120", "0x3d80b31a78c30fc628f20b2c89d7ddbf6e53cedc"]
```

#### personal\_listWallets <a href="#personal-listwallets" id="personal-listwallets"></a>

Returns a list of wallets this node manages.

| CLIENT  | METHOD INVOCATION                                  |
| ------- | -------------------------------------------------- |
| Console | personal.listWallets                               |
| RPC     | {"method": "personal\_listWallets", "params": \[]} |

**Example**

```javascript
> personal.listWallets
[{
  accounts: [{
    address: "0x51594065a986c58d4698c23e3d932b68a22c4d21",
    url: "keystore:///var/folders/cp/k3x0xm3959qf9l0pcbbdxdt80000gn/T/go-ethereum-keystore65174700/UTC--2022-06-28T10-31-09.477982000Z--51594065a986c58d4698c23e3d932b68a22c4d21"
  }],
  status: "Unlocked",
  url: "keystore:///var/folders/cp/k3x0xm3959qf9l0pcbbdxdt80000gn/T/go-ethereum-keystore65174700/UTC--2022-06-28T10-31-09.477982000Z--51594065a986c58d4698c23e3d932b68a22c4d21"
}]
```

#### personal\_lockAccount <a href="#personal-lockaccount" id="personal-lockaccount"></a>

Removes the private key with given address from memory. The account can no longer be used to send transactions.

| CLIENT  | METHOD INVOCATION                                        |
| ------- | -------------------------------------------------------- |
| Console | personal.lockAccount(address)                            |
| RPC     | {"method": "personal\_lockAccount", "params": \[string]} |

#### personal\_newAccount <a href="#personal-newaccount" id="personal-newaccount"></a>

Generates a new private key and stores it in the key store directory. The key file is encrypted with the given passphrase. Returns the address of the new account. At the geth console, newAccount will prompt for a passphrase when it is not supplied as the argument.

| CLIENT  | METHOD INVOCATION                                       |
| ------- | ------------------------------------------------------- |
| Console | personal.newAccount()                                   |
| RPC     | {"method": "personal\_newAccount", "params": \[string]} |

**Example**

```javascript
> personal.newAccount()
Passphrase:
Repeat passphrase:
"0x5e97870f263700f46aa00d967821199b9bc5a120"
```

The passphrase can also be supplied as a string.

```javascript
> personal.newAccount("h4ck3r")
"0x3d80b31a78c30fc628f20b2c89d7ddbf6e53cedc"
```

#### personal\_openWallet <a href="#personal-openwallet" id="personal-openwallet"></a>

Initiates a hardware wallet opening procedure by establishing a USB connection and then attempting to authenticate via the provided passphrase. Note, the method may return an extra challenge requiring a second open (e.g. the Trezor PIN matrix challenge).

| CLIENT  | METHOD INVOCATION                                               |
| ------- | --------------------------------------------------------------- |
| Console | personal.openWallet(url, passphrase)                            |
| RPC     | {"method": "personal\_openWallet", "params": \[string, string]} |

#### personal\_unlockAccount <a href="#personal-unlockaccount" id="personal-unlockaccount"></a>

Decrypts the key with the given address from the key store.

Both passphrase and unlock duration are optional when using the JavaScript console. If the passphrase is not supplied as an argument, the console will prompt for the passphrase interactively. The unencrypted key will be held in memory until the unlock duration expires. If the unlock duration defaults to 300 seconds. An explicit duration of zero seconds unlocks the key until geth exits.

The account can be used with eth\_sign and eth\_sendTransaction while it is unlocked.

| CLIENT  | METHOD INVOCATION                                                          |
| ------- | -------------------------------------------------------------------------- |
| Console | personal.unlockAccount(address, passphrase, duration)                      |
| RPC     | {"method": "personal\_unlockAccount", "params": \[string, string, number]} |

**Examples**

```javascript
> personal.unlockAccount("0x5e97870f263700f46aa00d967821199b9bc5a120")
Unlock account 0x5e97870f263700f46aa00d967821199b9bc5a120
Passphrase:
true
```

Supplying the passphrase and unlock duration as arguments:

```javascript
> personal.unlockAccount("0x5e97870f263700f46aa00d967821199b9bc5a120", "foo", 30)
true
```

To type in the passphrase and still override the default unlock duration, pass null as the passphrase.

```javascript
> personal.unlockAccount("0x5e97870f263700f46aa00d967821199b9bc5a120", null, 30)
Unlock account 0x5e97870f263700f46aa00d967821199b9bc5a120
Passphrase:
true
```

#### personal\_unpair <a href="#personal-unpair" id="personal-unpair"></a>

Deletes a pairing between wallet and Geth.

| CLIENT  | METHOD INVOCATION                                           |
| ------- | ----------------------------------------------------------- |
| Console | personal.unpair(url, pin)                                   |
| RPC     | {"method": "personal\_unpair", "params": \[string, string]} |

#### personal\_sendTransaction <a href="#personal-sendtransaction" id="personal-sendtransaction"></a>

Validate the given passphrase and submit transaction.

The transaction is the same argument as for eth\_sendTransaction (i.e. [transaction object](https://geth.ethereum.org/docs/interacting-with-geth/rpc/objects#transaction-call-object)) and contains the from address. If the passphrase can be used to decrypt the private key belogging to tx.from the transaction is verified, signed and send onto the network. The account is not unlocked globally in the node and cannot be used in other RPC calls.

| CLIENT  | METHOD INVOCATION                                                |
| ------- | ---------------------------------------------------------------- |
| Console | personal.sendTransaction(tx, passphrase)                         |
| RPC     | {"method": "personal\_sendTransaction", "params": \[tx, string]} |

**Examples**

```javascript
> var tx = {from: "0x391694e7e0b0cce554cb130d723a9d27458f9298", to: "0xafa3f8684e54059998bc3a7b0d2b0da075154d66", value: web3.toWei(1.23, "ether")}
undefined
> personal.sendTransaction(tx, "passphrase")
0x8474441674cdd47b35b875fd1a530b800b51a5264b9975fb21129eeb8c18582f
```

#### personal\_sign <a href="#personal-sign" id="personal-sign"></a>

The sign method calculates an Ethereum specific signature with: sign(keccak256("\x19Ethereum Signed Message:\n" + len(message) + message)).

By adding a prefix to the message makes the calculated signature recognisable as an Ethereum specific signature. This prevents misuse where a malicious DApp can sign arbitrary data (e.g. transaction) and use the signature to impersonate the victim.

See ecRecover to verify the signature.

| CLIENT  | METHOD INVOCATION                                                     |
| ------- | --------------------------------------------------------------------- |
| Console | personal.sign(message, account, \[password])                          |
| RPC     | {"method": "personal\_sign", "params": \[message, account, password]} |

**Examples**

```javascript
> personal.sign("0xdeadbeaf", "0x9b2055d370f73ec7d8a03e965129118dc8f5bf83", "")
"0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b"
```

#### personal\_signTransaction <a href="#personal-signtransaction" id="personal-signtransaction"></a>

SignTransaction will create a transaction from the given arguments and tries to sign it with the key associated with tx.from. If the given passwd isn't able to decrypt the key it fails. The transaction is returned in RLP-form, not broadcast to other nodes. The first argument is a [transaction object](https://geth.ethereum.org/docs/interacting-with-geth/rpc/objects) and the second argument is the password, similar to personal\_sendTransaction.

| CLIENT  | METHOD INVOCATION                                                |
| ------- | ---------------------------------------------------------------- |
| Console | personal.signTransaction(tx, passphrase)                         |
| RPC     | {"method": "personal\_signTransaction", "params": \[tx, string]} |

#### personal\_ecRecover <a href="#personal-ecrecover" id="personal-ecrecover"></a>

ecRecover returns the address associated with the private key that was used to calculate the signature in personal\_sign.

| CLIENT  | METHOD INVOCATION                                                  |
| ------- | ------------------------------------------------------------------ |
| Console | personal.ecRecover(message, signature)                             |
| RPC     | {"method": "personal\_ecRecover", "params": \[message, signature]} |

**Examples**

```javascript
> personal.sign("0xdeadbeaf", "0x9b2055d370f73ec7d8a03e965129118dc8f5bf83", "")
"0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b"
> personal.ecRecover("0xdeadbeaf", "0xa3f20717a250c2b0b729b7e5becbff67fdaef7e0699da4de7ca5895b02a170a12d887fd3b17bfdce3481f10bea41f45ba9f709d39ce8325427b57afcfc994cee1b")
"0x9b2055d370f73ec7d8a03e965129118dc8f5bf83"
```
