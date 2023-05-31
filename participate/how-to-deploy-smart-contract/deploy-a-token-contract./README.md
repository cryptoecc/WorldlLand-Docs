# Use Remix IDE

### 1. [Connect wallet to Worldland network](../../../use/how-to-connect-wallet-to-worldland-network.md)

### 1.1 ❗️ Fund your WorldLand

When deploying contracts, you need some coins. This a way how to get world land testnet coins! Plz follow these [statements](https://ethworldland.gitbook.io/ethereum-worldland/use/how-to-obtain-your-wlcs-the-worldland-coins):



### 2. Run the remix and compile the code

Remix-IDE: https://remix-project.org/

2.1 make file and input file name&#x20;

any name is okay

\[image]

2.2 write or Paste contract code&#x20;

I use this code samples

2.2.1 fungible tokens

```
// contracts/ testerc20.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract TESTToken is ERC20 {
    constructor(uint256 initialSupply) ERC20("TEST", "TST") {
        _mint(msg.sender, initialSupply);
    }
}
```

2.2.2 Non-fungible tokens

```
// contracts/testerc721.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract TESTItem is ERC721URIStorage {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIds;
    
    constructor() ERC721("TESTItem", "TST") {}
    
    function awardItem(address player, string memory tokenURI)
        public
        returns (uint256)
    {
        _tokenIds.increment();
        uint256 newItemId = _tokenIds.current();
        _mint(player, newItemId);
        _setTokenURI(newItemId, tokenURI);
        return newItemId;
    }
}
```

When you're done writing the code, go to the Compile tab.

\[image]

### 3. Connect to Metamask and deploy to contract

After compiling, go to the Deployment tab.

\[image]

Select "injected web3" in the environment.

\[image]

The connected network number and account will then appear.

\[image]

If there are parameters of the contract constructor, write them by clicking the button in the picture below.

\[image]

Click the TRANSACT button to deploy the contract.&#x20;

If deploy fails because there is no ether in ETH-ECC, you can obtain ether from the free-eth page of explorer.&#x20;

Ethereum Block Explorer (desecure.org)&#x20;

If the free full balance is 0, you can tell me (Seung-min Kim).

\[image]

Finally, you can deploy contract to ETH-ECC

\[image]



### 4. Execute function of contract

You can excute function of contract in Deployed Contracts

### 5. Import token in metamask

You can check your tokens in metamsk using "Import tokens"

\[image]

Extra. Save nft using ipfs(pinata)

&#x20;Below is how to register NFT using pinata and ipfs in erc721.&#x20;

If the above TEST721.sol contract is deployed, the following functions appear.

\[image]

awarditem is a function that awards the NFT json file in tokenUrl to the player.

So, we need to store the JSON file in the URL.&#x20;

Upload the NFS JSON file to IPFS using pinata.

1. First sign up for Pinata

{% embed url="https://www.pinata.cloud/" %}

2\. upload image of nft and make json The format of the json file is as follows.

```
{
"name": "timetable",
"description": "smin's timetable",
"image":
"https://gateway.pinata.cloud/ipfs/QmWnNt8jdSxVX981abPHKTAsg5E31u2Zh8AfsVqzhyGzS
k",
"strength": 20
}
```

If you want to include an image, the image must also be stored in ipfs. So, I upload the image first.

\[image]

You can see the file is saved. Click the eye icon and copy the url of the image. ex: https://gateway.pinata.cloud/ipfs/QmWUR3PYmorqqQ2mGwQAr3ujUNnpANS2xyKJYBxegwFeS8

\[image]

Paste the url into the image item in json. "image": "https://gateway.pinata.cloud/ipfs/QmWnNt8jdSxVX981abPHKTAsg5E31u2Zh8AfsVqzhyGzSk",

3\. Upload the json to pinata and copy the url. The method is the same as the image.

\[image]

Finally, copy the address of your wallet, put your wallet address in the player, and the json url in tokenURL and send the transaction.

\[image]

You saved the NFT! If you want to check nft, see " HOW TO CHECK NFT SMART CONTRACT IN ETH-ECC "



