---
description: >-
  After reading this page, you can create, compile and deploy an NFT smart
  contract using Truffle.
---

# Use Truffle

## Setting up the development environment

### Prerequisites

* [VS Code installed](https://code.visualstudio.com/download)
* [Node.js(+npm) installed](https://nodejs.org/en/)
* [Git](https://git-scm.com/downloads)
* Make your own [MetaMask](https://drive.google.com/file/d/1fHLjr5VJfe\_HaSFClLPb-psawsxb0SAo/view) or similar to create a wallet

{% hint style="info" %}
Check your environment and install using that link.
{% endhint %}

## Steps

### 1. Fund your WorldLand

When deploying contracts, you need some coins. This a way how to get world land testnet coins! Plz follow these [statements](https://ethworldland.gitbook.io/ethereum-worldland/use/how-to-send-and-receive-coins.):

### 2. Install Truffle

NOW, We start to install "Truffle" using the Node.js package manager on VS Code Terminal:

```bash
// VS Code Terminal: cmd
npm install -g truffle
```

{% hint style="info" %}
#### Better save your own time!

When installing all packages, Run the _command prompt_(_CMD_) with administrator privileges.
{% endhint %}

### 3. Install `dotenv` package&#x20;

```bash
// VS Code Terminal: cmd
npm install dotenv
```

### 4. Install `@truffle/hdwallet-provider`

```bash
// VS Code Terminal: cmd
npm install @truffle/hdwallet-provider
```

### 5. Install OpenZepplin

```bash
// VS Code Terminal: cmd
npm install --save-dev @openzeppelin/contracts
```

### 5. Open your project directory on VS Code

Create "newNFT" folder and move to "newNFT" folder.

```bash
// VS Code Terminal: cmd
mkdir newNFT
cd newNFT
```

### 6. Create the .env file

Create a ".env" file and writing your metamask and other information.

