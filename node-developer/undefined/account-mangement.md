# Account Mangement

Account security is very important in blockchain networks. You should make sure that your account's private key and password are inaccessible to anyone but yourself. If someone else obtains your account's private key and password, they can control all assets associated with your account. You should safely back up your account. If you lose your key file or password, your account assets are inaccessible and permanently lost.

ETH-ECC's node client has an internal account management tool. However, for better security, an off-client account management tool is desirable. Clef, an external account management tool supported by ETH-ECC, can be run separately from the client and operates on independent hardware. Clef requires manual review of account-related actions by the owner, and is more secure than traditional account management because signing is done inside Clef.

{% hint style="warning" %}
**Keep your account safe and backed up!**
{% endhint %}



## Clef

### **Clef init**

Clef must be initialized before creating an account. Determine the path for Clef and pass the repository path to the clef init command.

```sh
$ ./clef init /CLEF_DIR/clefdata
```

{% hint style="info" %}
Please remember the master seed generated and keep it safe. The master seed gives you access to the account managed by clef.
{% endhint %}



### Connecting ETH-ECC and Clef

In order for Clef and ETH-ECC to communicate with each other, Cleft needs to know the chain ID of the network and the location of the node's keystore. Keystores are usually located inside the node data directory.

To enable communication with Clef using Curl, you can pass --http which by default starts an HTTP server at localhost:8550. Run the following command to start a Clef configured for ETH-ECC nodes connecting to the Seoul mainnet.

```sh
$ ./clef -chainid 103 -keystore ~/ETH-ECC_DIR/keystore -configdir /CLEF_DIR/clef --http
```



Clef starts running in the terminal, starting with a disclaimer and prompting to click "OK".

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

ETH-ECC can be started in a separate terminal. To connect to Clef, make sure the data directory matches the path provided to Clef and pass the location of the Clef IPC file. Clef saves this file to the path provided in the -configdir flag.

<pre class="language-sh"><code class="lang-sh"><strong>$ ./worldland &#x3C;other flags> -signer=/CLEF_DIR/clef/clef.ipc
</strong></code></pre>

### **New Account** <a href="#interacting-with-clef" id="interacting-with-clef"></a>

A new key file has been added to the keystore for ETH-ECC . A JSON response is returned with the new account address in the result field.

```
{"jsonrpc": "2.0", "id": 0, "result": "0x168bc315a2ee09042d83d7c5811b533620531f67"}
```



The newly created key file can be found in /keystore/, a subfolder of the node directory. The file name includes the key generation date and time and address.&#x20;

For example:

```
UTC--2022-05-19T12-34-36.47413510Z--0b85e5a13e118466159b1e1b6a4234e5f9f784bb
```

You can also create an account by importing the user's existing hexadecimal private key.

```sh
$ ./clef importraw <hexkey>
```



### List accounts

In the clef console, you can use the following CLI command to list your accounts.

```sh
./clef list-accounts --keystore <path-to-keystore>
```

This will return a JSON object with your account address.

You can also list accounts using `eth.accounts` but require authorization from Clef.

You can list all wallets managed by clef with the following command

```sh
./clef list-wallets --keystore <path-to-keystore>
```

returns:



### Import account

Clef also supports creating an account using a pre-existing private key. You can bring the address created in a wallet such as Metamask to Clef and interact with it. You can import your account by running the command below and entering your password. Like I said, protect your passwords and back them up.

```sh
$ ./worldland account import -datadir /YOUR_DIR ./KEY_DIR
```

The following information is displayed in the terminal indicating a successful import.



### Account update

Clef can be used to set and remove passwords for existing keystore files. To set a new password, pass the account address to setpw.

```sh
$ ./clef setpw YOUR_ACCOUNT_ADDRESS
```

This will cause Clef to enter the new password twice, followed by the Clef master password to decrypt the key file.



{% hint style="info" %}
See the [clef](https://geth.ethereum.org/docs/tools/clef/introduction) section of the go-ethereum docs for details.
{% endhint %}

