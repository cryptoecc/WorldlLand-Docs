# Testing Worldland

#### _Please contact us if you have any questions._ __[_https://open.kakao.com/o/gXdk2J5e_](https://open.kakao.com/o/gXdk2J5e)__



1. Basic tests
   * making an account, mining block and checking result of mining
2. Making a transaction
3. (Appendix) Block generation time log

#### 3.1 Basic tests

In this test, we will follow 3 steps

* Generate account
* Check account's balance
* Mining

**Generating account**

Generating new account:

```
> personal.newAccount("Alice")
```

returns data that looks like:

```
INFO [08-06|21:33:36.241] Your new key was generated               address=0xb8C941069cC2B71B1a00dB15E6E00A200d387039
WARN [08-06|21:33:36.241] Please backup your key file!             path=/home/hskim/Documents/geth-test/keystore/UTC--2019-08-06T12-33-34.442823142Z--b8c941069cc2b71b1a00db15e6e00a200d387039
WARN [08-06|21:33:36.241] Please remember your password! 
"0xb8c941069cc2b71b1a00db15e6e00a200d387039"
```

We generated the address of Alice:`0xb8C941069cC2B71B1a00dB15E6E00A200d387039`. You can check the account using the following command.

```
> eth.accounts
["0xb8c941069cc2b71b1a00db15e6e00a200d387039"]
```

we will use it as miner's address so block generation reward will be sent to Alice's address that "0xb8c941069cc2b71b1a00db15e6e00a200d387039"

**Check account's balance**

Before mining, To calculate the amount of ethers mined, you have to check current balance of miner's account. You can check the balance by the following commands.

```
> eth.getBalance("0xb8c941069cc2b71b1a00db15e6e00a200d387039")
0
```

Or use

```
> eth.getBalance(eth.accounts[0])
0
```

**Mining**

First we have to set miner's address. For this, we will use 3 commands

* miner.setEtherbase(address)
  * It sets miner's address. Mining reward will be sent to this account
* miner.start(number of threads)
  * Start mining. You can set how many threads you will use. I will use 1 thread
  * If your CPU has enough core, you can use higher number. It will work faster.
* miner.stop()
  * Stop mining

Setting miner's address:

```
> miner.setEtherbase("0xb8c941069cc2b71b1a00db15e6e00a200d387039")
true
```

Starting mining:

```
> miner.start(1)
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

After mining, check the amount of mined ethers:

```
> eth.getBalance("0xb8c941069cc2b71b1a00db15e6e00a200d387039")
45000000000000000000
```

Exactly wei, not ether that `10^18 wei` is equal to `1 ether`. wei is small unit of ether like satoshi of bitcoin. In order to show the balance in ether use the below command.

```
> web3.fromWei(eth.getBalance("0xb8c941069cc2b71b1a00db15e6e00a200d387039"), "ether")
45
```

#### 3.2 Making a transaction for test in private network

In this section, we create another account to generate a transaction and send ether. We will make a new account(Bob) and send ether from miner(Alice) to new account(Bob)

Generating new account:

```
> personal.newAccount("Bob")
INFO [08-06|22:00:23.416] Your new key was generated               address=0xf39Cf42Cd233261cd2b45ADf8fb1E5A1e61A6f90
WARN [08-06|22:00:23.416] Please backup your key file!             path=/home/hskim/Documents/geth-test/keystore/UTC--2019-08-06T13-00-21.621172635Z--f39cf42cd233261cd2b45adf8fb1e5a1e61a6f90
WARN [08-06|22:00:23.416] Please remember your password! 
"0xf39cf42cd233261cd2b45adf8fb1e5a1e61a6f90"

> eth.getBalance("0xf39cf42cd233261cd2b45adf8fb1e5a1e61a6f90")
0
```

I got account of Bob:`0xf39cf42cd233261cd2b45adf8fb1e5a1e61a6f90`. Alice will send ether to Bob's account. Before sending, we have to unlock fowarding account(Alice).

Status of Alice's account.

```
> personal.listWallets[0].status
"Locked"
```

Unlocking:

```
> web3.personal.unlockAccount("0xb8c941069cc2b71b1a00db15e6e00a200d387039")
Unlock account 0xb8c941069cc2b71b1a00db15e6e00a200d387039
```

if an error occurs. When running ./geth, add the **--allow-insecure-unlock** option

**\[WARNING]** Using this option for nodes expose to **public networks** have a **security risk.**

```
 ./geth ... --allow-insecure-unlock ... conosle
```



Alice's address is `0xb8c941069cc2b71b1a00db15e6e00a200d387039`. However we have to type a `Passphrase` that is `Alice`.

```
Passphrase: Alice
true
```

Now Alice's account is unlocked. Then let's make transaction that sending 5 ether from Alice to Bob.

```
> eth.sendTransaction({from: "0xb8c941069cc2b71b1a00db15e6e00a200d387039", to: "0xf39cf42cd233261cd2b45adf8fb1e5a1e61a6f90", value: web3.toWei(5, "ether")})
```

Or we can initialize these using variable

```
> from = "0xb8c941069cc2b71b1a00db15e6e00a200d387039"
> to = "0xb8c941069cc2b71b1a00db15e6e00a200d387039"
> eth.sendTransaction({from: from, to: to, value: web3.toWei(5, "ether")})
```

then those returns data that looks like:

```
INFO [08-06|22:16:09.274] Setting new local account                address=0xb8C941069cC2B71B1a00dB15E6E00A200d387039
INFO [08-06|22:16:09.275] Submitted transaction                    fullhash=0x926f1bb71d5b48a306e6cde2d45c01f8af2107febf94b166a7e5f8e025dc8adc recipient=0xf39Cf42Cd233261cd2b45ADf8fb1E5A1e61A6f90
"0x926f1bb71d5b48a306e6cde2d45c01f8af2107febf94b166a7e5f8e025dc8adc"
```

Checking a pending transactions

```
> eth.pendingTransactions
[{
    blockHash: null,
    blockNumber: null,
    from: "0xb8c941069cc2b71b1a00db15e6e00a200d387039",
    gas: 21000,
    gasPrice: 1000000000,
    hash: "0x926f1bb71d5b48a306e6cde2d45c01f8af2107febf94b166a7e5f8e025dc8adc",
    input: "0x",
    nonce: 0,
    r: "0x70484271bdc85f7233e715423d8d0be5c669a323385b5ec0ff080a52cf3c654c",
    s: "0x1b55a792995f61128c10a48ce1e0869893c863d38489f574d84ae3a96b031cef",
    to: "0xf39cf42cd233261cd2b45adf8fb1e5a1e61a6f90",
    transactionIndex: null,
    v: "0x42",
    value: 5000000000000000000
}]
```

However, the transaction has not yet been written to the block., cause we didn't mine any block to store the pending transaction.

```
> eth.getBalance("0xb8c941069cc2b71b1a00db15e6e00a200d387039")
45000000000000000000
> eth.getBalance("0xf39cf42cd233261cd2b45adf8fb1e5a1e61a6f90")
0
```

Mining the next block:

```
> miner.start(1)
INFO [08-06|22:19:53.061] Updated mining threads                   threads=1
INFO [08-06|22:19:53.061] Transaction pool price threshold updated price=1000000000
null
> INFO [08-06|22:19:53.062] Commit new mining work                   number=10 sealhash=f69cfb…273c0d uncles=0 txs=0 gas=0 fees=0 elapsed=265.557µs
INFO [08-06|22:19:53.062] Commit new mining work                   number=10 sealhash=a018f5…65f494 uncles=0 txs=1 gas=21000 fees=2.1e-05 elapsed=1.022ms
INFO [08-06|22:19:54.718] Successfully sealed new block            number=10 sealhash=a018f5…

.
.
.

INFO [08-06|22:20:05.086] 🔨 mined potential block                  number=16 hash=e7688a…09ed64
INFO [08-06|22:20:05.086] Commit new mining work                   number=17 sealhash=6b297d…b76b19 uncles=0 txs=0 gas=0     fees=0       elapsed=252.945µs
> miner.stop()
null
```

Last time Alice mined 9 blocks and this time mined 7 blocks more. So We can expect Alice has 75 ether (80 ether block reward - 5 ether sent to Bob = 75 ether). Let's check.

```
> eth.pendingTransactions
[]
```

There is no pending transaction. It means that Alice and Bob's transaction is done.

Let's see the balance of them

```
> eth.getBalance("0xb8c941069cc2b71b1a00db15e6e00a200d387039")
75000000000000000000
> eth.getBalance("0xf39cf42cd233261cd2b45adf8fb1e5a1e61a6f90")
5000000000000000000
```

As we expected, Alice has 75 ether and Bob has 5 ether.
