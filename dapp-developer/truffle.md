# Truffle

## Use Truffle

### Setting up the development environment

#### Prerequisites

* [VS Code installed](https://code.visualstudio.com/download)
* [Node.js(+npm) installed](https://nodejs.org/en/)
* [Git](https://git-scm.com/downloads)
* Make your own [MetaMask](https://drive.google.com/file/d/1fHLjr5VJfe\_HaSFClLPb-psawsxb0SAo/view) or similar to create a wallet

\{% hint style="info" %\} Check your environment and install using that link. \{% endhint %\}

### Steps

#### 1. Fund your WorldLand

When deploying contracts, you need some coins. This a way how to get world land testnet coins! Plz follow these [statements](https://ethworldland.gitbook.io/ethereum-worldland/use/how-to-send-and-receive-coins.):

#### 2. Install Truffle

NOW, We start to install "Truffle" using the Node.js package manager on VS Code Terminal:

```
// VS Code Terminal: cmd
npm install -g truffle
```

\{% hint style="info" %\}

**Better save your own time!**

When installing all packages, Run the _command prompt_(_CMD_) with administrator privileges. \{% endhint %\}

#### 3. Install `dotenv` package

```
// VS Code Terminal: cmd
npm install dotenv
```

#### 4. Install `@truffle/hdwallet-provider`

```
// VS Code Terminal: cmd
npm install @truffle/hdwallet-provider
```

#### 5. Install OpenZepplin

```
// VS Code Terminal: cmd
npm install --save-dev @openzeppelin/contracts
```

#### 5. Open your project directory on VS Code

Create `"newNFT"` folder and move it to `"newNFT"` folder.

```
// VS Code Terminal: cmd
mkdir newNFT
cd newNFT
```

\{% hint style="success" %\} Check directory. It may be similar to below: \{% endhint %\}

```
// Directory structure
│
├─ addition-game-starter
│
├─ build
│
├─ contracts
│
├─ migrations
│
├─ node_modules
│
└─ test
package-lock.json
package.json
truffle-config.js
```

#### 6. Create the `.env` file

Create a ".env" file and write your MetaMask secret recovery phrase and others.

\{% hint style="danger" %\} You must keep your _**"MNEMONIC"**_ key. Never show your information. \{% endhint %\}

```
//.env 
MNEMONIC = *Your-MetaMask-Secret-Recovery-Phrase*
```

#### 7. Edit `truffle-config.js` file

`truffle-config.js` file needs to configure some information about specific things.

Find `module.export` part.

```
// write require('dotenv').config()
require('dotenv').config()
const HDWalletProvider = require('@truffle/hdwallet-provider')
const { MNEMONIC, PROJECT_ID } = process.env;
// Modify specific network information
module.exports = {
    networks: {
        worldland: {
            provider: () => new HDwalletProvider(MNEMONIC,'https://rpc.lvscan.io/')
            network_id: 12345,
            gas: 5500000,
        }
    },
    mocha: {
      // timeout: 100000
      },
    compilers: {
        solc: {
          version: "0.8.13" // Fetch exact version from solc-bin (default: truffle's version)
          // docker: true,        // Use "0.5.1" you've installed locally with docker (default: false)
          // settings: {          // See the solidity docs for advice about optimization and evmVersion
          //  optimizer: {
          //    enabled: false,
          //    runs: 200
          //  },
          //  evmVersion: "byzantium"
          // }
        }
    },
};
```

#### 8. Create a smart content

You can edit this code to your style. This code is just an example. I'll give you two types.

The below codes are the `first type`. The `first type` is the general type. You can choose it generally.

```
// First type
// Contract based on [https://docs.openzeppelin.com/contracts/4.x/erc721](https://docs.openzeppelin.com/contracts/4.x/erc721)
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "@openzeppelin/contracts/utils/Counters.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract newNFT is ERC721URIStorage, Ownable {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIds;

    constructor() ERC721("newNFT", "NFT") {}

    function mintNFT(address recipient, string memory tokenURI)
        public
        returns (uint256)
    {
        _tokenIds.increment();

        uint256 newItemId = _tokenIds.current();
        _safeMint(recipient, newItemId);
        _setTokenURI(newItemId, tokenURI);

        return newItemId;
    }
}
```

The below codes are the `Second type`.

```
// Second type
// Contract based on (https://docs.openzeppelin.com/contracts/4.x/erc721)
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

import "@openzeppelin/contracts-upgradeable/token/ERC721/ERC721Upgradeable.sol";
import "@openzeppelin/contracts-upgradeable/token/ERC721/extensions/ERC721URIStorageUpgradeable.sol";
import "@openzeppelin/contracts-upgradeable/access/OwnableUpgradeable.sol";
import "@openzeppelin/contracts-upgradeable/proxy/utils/Initializable.sol";
import "@openzeppelin/contracts-upgradeable/utils/CountersUpgradeable.sol";

/*Smart contracts are immutable by default unless deployed behind an upgradeable proxy
(https://docs.openzeppelin.com/upgrades)*/

contract MyToken is Initializable, ERC721Upgradeable, ERC721URIStorageUpgradeable, OwnableUpgradeable {
    using CountersUpgradeable for CountersUpgradeable.Counter;
    CountersUpgradeable.Counter private _tokenIdCounter;
    /// @custom:oz-upgrades-unsafe-allow constructor
    constructor() {
        _disableInitializers();
    }
    function initialize() initializer public {
        __ERC721_init("MyToken", "MTK");
        __ERC721URIStorage_init();
        __Ownable_init();
    }
    function safeMint(address to, string memory uri) public onlyOwner {
        uint256 tokenId = _tokenIdCounter.current();
        _tokenIdCounter.increment();
        _safeMint(to, tokenId);
        _setTokenURI(tokenId, uri);
    }
    // The following functions are overrides required by Solidity.
    function _burn(uint256 tokenId)
        internal
        override(ERC721Upgradeable, ERC721URIStorageUpgradeable)
    {
        super._burn(tokenId);
    }
    function tokenURI(uint256 tokenId)
        public
        view
        override(ERC721Upgradeable, ERC721URIStorageUpgradeable)
        returns (string memory)
    {
        return super.tokenURI(tokenId);
    }
}
```

#### 9. Write `1_initial_newNFT.js`

* Make `1_initial_newNFT.js` under migrations folder
* Write specific codes on `1_initial_newNFT.js`

```
var newNFT = artifacts.require("newNFT.sol")

module.exports = function(deployer) {
  deployer.deploy(newNFT);
};
```

#### 10. Compile the smart contract

```
// compile contract
truffle compile
```

When successfully compile, you can see like below:

```
Compiling your contracts...
===========================
> Compiling .\contracts\newNFT.sol
> Compiling .\contracts\newNFT.sol
> Artifacts written to C:\Users\SuminKim\Desktop\newNFT\nft\build\contracts
> Compiled successfully using:
   - solc: 0.8.13+commit.abaa5c0e.Emscripten.clang
```

#### 11. Deploy your contract on `WorldLand` network

```
// Deploy contract
truffle migrate --network worldland
```

When successfully compile, you can see like below:

```
Compiling your contracts...
===========================
> Compiling .\contracts\newNFT.sol
> Compiling .\contracts\newNFT.sol
> Artifacts written to C:\Users\SuminKim\Desktop\newNFT\nft\build\contracts
> Compiled successfully using:
   - solc: 0.8.13+commit.abaa5c0e.Emscripten.clang


Starting migrations...
======================
> Network name:    'worldland'
> Network id:      12345
> Block gas limit: 30000000 (0x1c9c380)


1_initial_newNFT.js
===================

   Replacing 'newNFT'
   ------------------
   > transaction hash:    0x9dc71d5c4742af53b62eaf5099918ab349aa0b03b0827530a3f7c4903c3c0bd8
   > Blocks: 0            Seconds: 228
   > contract address:    0x07cc033F14e16Ced9d21ee49279C37b7cEB4832a
   > block number:        10615
   > block timestamp:     1674041065
   > account:             0x68Eb38DC93190362785Df115891a3FF04a90C5af
   > balance:             9.979944564943844782
   > gas used:            2674034 (0x28cd72)
   > gas price:           2.500000007 gwei
   > value sent:          0 ETH
   > total cost:          0.006685085018718238 ETH

   > Saving artifacts
   -------------------------------------
   > Total cost:     0.006685085018718238 ETH

Summary
=======
> Total deployments:   1
> Final cost:          0.006685085018718238 ETH
```

#### 12. Finally, check contract on [explore](http://3.39.29.150:3000/?network=ETH-ECC)

Copy block number(10615) and check it on [explore(LV Scanner)](http://3.39.29.150:3000/block/0x4aab14e298e8b3c01dd6d56ea056b8e8cb24f501c730ec661efd546e79b9acce?network=ETH-ECC)!

[![image](https://github.com/cryptoecc/WorldlLand-Docs/raw/master/.gitbook/assets/deployed.PNG)](../.gitbook/assets/deployed.PNG)

\{% hint style="success" %\} You can confirm Timestamp, Hash, and others about your contract. \{% endhint %\}
