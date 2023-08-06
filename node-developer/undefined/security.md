# Security



Since the Worldland blockchain network is a peer-to-peer network, it must be able to communicate with all nodes. The default port settings of ETH-ECC are as follows.

| Communication | Port  |
| ------------- | ----- |
| P2P           | 30303 |
| HTTP-RPC      | 8545  |
| WS-RPC        | 8546  |

The P2P network is set by default, and HTTP and WebSocket (WS) are disabled by default unless the command is enabled.



The network firewall settings for Worldland network nodes are as follows:

* Allow traffic on TCP 30303 or a custom port defined for peer-to-peer communication. This allows nodes to connect to peers.
* Allow traffic on UDP 30303 or a custom port defined for peer-to-peer communication. This allows node discovery.

If enabling a JSON-RPC server, include the settings below.

{% hint style="info" %}
When enabling **RPC servers** on Worldland nodes, security must be taken into account. When a node allows external access, an attacker with an unlocked account can easily transfer the ether stored in the wallet.



Please refer to the link below:

[https://ethereum.stackexchange.com/questions/3887/how-to-reduce-the-chances-of-your-ethereum-wallet-getting-hacked](https://ethereum.stackexchange.com/questions/3887/how-to-reduce-the-chances-of-your-ethereum-wallet-getting-hacked)
{% endhint %}

* Block all traffic to 8545 or all custom ports defined for JSON-RPC requests to the node (except traffic from explicitly defined trusted systems).
* Block all traffic to 8546 or all custom ports defined for JSON-RPC requests to the node (except traffic from explicitly defined trusted systems).



If you want to change the **P2P port**, see the `-port` options in Command Line Options.

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



