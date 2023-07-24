# Connect to Metamask

This part explains how to link your Metamask account to the Eth-ECC console and link your Eth-ECC account to Metamask.

### Metamask account  to Eth-ECC

You can find **Account details** in the menu to the right of your **Metamask account**.

<figure><img src="../../.gitbook/assets/account_details.png" alt=""><figcaption></figcaption></figure>

Press the **export private key** button and enter the **password** to obtain the private key.

<figure><img src="../../.gitbook/assets/export_private_key.png" alt=""><figcaption></figcaption></figure>

Enter the obtained **private key** and **password** into the **ETH-ECC** console.

`web3.personal.importRawKey("PRIVATE_KEY", "METAMASK_PASSWORD")`

```
> eth.accounts
["0xb8c941069cc2b71b1a00db15e6e00a200d387039"]
```

then can you check account :)

### ETH-ECC account to metamask

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

We generated the address of Alice:`0xb8C941069cC2B71B1a00dB15E6E00A200d387039`. You can check the account using the following command.

```
> eth.accounts
["0xb8c941069cc2b71b1a00db15e6e00a200d387039"]
```



You can find your key file in [`YOUR_GETH_DATADIR/keystore`](#user-content-fn-1)[^1]

If not configured, the data storage location is `~/.ethereum.`

<figure><img src="https://raw.githubusercontent.com/cryptoecc/WorldlLand-Docs/master/.gitbook/assets/UTCFILE.png" alt=""><figcaption></figcaption></figure>

Save the file in **json format**. `UTC--2023....json`

Open metamask, select the network and then select "Import Account"

<figure><img src="https://raw.githubusercontent.com/cryptoecc/WorldlLand-Docs/master/.gitbook/assets/import%20account.png" alt=""><figcaption></figcaption></figure>

Select JSON File from Select Type and import the file. And enter the password you entered when creating your account.

<figure><img src="../../.gitbook/assets/import_json.png" alt=""><figcaption></figcaption></figure>

then, you can import account to **Metamask!**





[^1]: 