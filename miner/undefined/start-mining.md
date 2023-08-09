---
description: This document describes a quick running guide for Miner
---

# Start Mining

### **Generating account**

Generating new account:

```
> personal.newAccount("YOUR_PASSWORD")
```

returns data that looks like:

```
INFO [08-06|21:33:36.241] Your new key was generated               address=0xb8C941069cC2B71B1a00dB15E6E00A200d387039
WARN [08-06|21:33:36.241] Please backup your key file!             path=/home/hskim/Documents/geth-test/keystore/UTC--2019-08-06T12-33-34.442823142Z--b8c941069cc2b71b1a00db15e6e00a200d387039
WARN [08-06|21:33:36.241] Please remember your password! 
"0xb8c941069cc2b71b1a00db15e6e00a200d387039"
```

**`personal.newAccount("YOUR_PASSWORD")`** returns your **wallet address.**  The example above returned the wallet address **`"0xb8c941069cc2b71b1a00db15e6e00a200d387039"`**.

{% hint style="warning" %}
**Be careful not to forget your password!**
{% endhint %}

{% hint style="info" %}
You can improve account security by utilizing **Clef**, an external account management tool. See the [Security ](../../node-developer/undefined/security.md)topic for details.
{% endhint %}

You can check the list of **currently added wallet addresses** via the **`eth.accounts`** command.

```
> eth.accounts
["0xb8c941069cc2b71b1a00db15e6e00a200d387039"]
```

### Mining

**Check account's balance**

Before mining, To calculate the amount of **WLCs** mined, you have to check current balance of miner's account. You can check the balance by the **eth.getBalance("YOUR\_ADDRESS")** commands.

```
> eth.getBalance("0xb8c941069cc2b71b1a00db15e6e00a200d387039")
0
```

Or use

```
> eth.getBalance(eth.accounts[0])
0
```

First we have to set miner's address. For this, we will use 3 commands

* **`miner.setEtherbase(address)`**
  * It sets miner's address. Mining reward will be sent to this account
* **`miner.start(number of threads)`**
  * Start mining. You can set how many threads you will use. I will use 1 thread
  * If your CPU has enough core, you can use higher number. It will work faster.
* **`miner.stop()`**
  * Stop mining

{% hint style="info" %}
GPU mining is not supported yet :(
{% endhint %}

**Setting miner's address:**

```
> miner.setEtherbase("0xb8c941069cc2b71b1a00db15e6e00a200d387039")
true
```

Starting mining:

```
> miner.start()
null
INFO [08-06|21:42:38.198] Updated mining threads                   threads=1
INFO [08-06|21:42:38.198] Transaction pool price threshold updated price=1000000000
null
> INFO [08-06|21:42:38.198] Commit new mining work                   number=1 sealhash=4bb421…3f463a uncles=0 txs=0 gas=0 fees=0 elapsed=325.066µs
INFO [08-06|21:42:40.752] Successfully sealed new block            number=1 sealhash=4bb421…3f463a hash=4b2b78…4808f6 elapsed=2.554s
INFO [08-06|21:42:40.752] 🔨 mined potential block                  number=1 hash=4b2b78…4808f6

.
.
.

INFO [08-06|21:42:56.174] 🔨 mined potential block                  number=9 hash=2faebb…8be693
INFO [08-06|21:42:56.174] Commit new mining work                   number=10 sealhash=384aa6…cb0596 uncles=0 txs=0 gas=0 fees=0 elapsed=179.463µs
```

Stopping mining:

```
> miner.stop()
null
```

After mining, check the amount of mined **WLCs**:

```
> eth.getBalance("0xb8c941069cc2b71b1a00db15e6e00a200d387039")
45000000000000000000
```

Exactly wei, not ether that `10^18 wei` is equal to `1 WLC`. wei is small unit of WLC like satoshi of bitcoin. In order to show the balance in ether use the below command.

```
> web3.fromWei(eth.getBalance("0xb8c941069cc2b71b1a00db15e6e00a200d387039"), "wlc")
45
```

###
