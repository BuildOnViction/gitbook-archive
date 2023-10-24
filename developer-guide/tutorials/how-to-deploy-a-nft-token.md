---
description: 'Create a unique ERC721-equivalent token (ie: CryptoKitties) on TomoChain!'
---

# How to deploy an NFT token

This article will explain:

* What is a Non-Fungible Token (NFT)
* Use-cases of NFT
* How-to step-by-step deploy a NFT token on TomoChain

What is a Non-Fungible Token (NFT)?

Fungible tokens are **all equal and interchangeable**. For instance, dollars or Bitcoins or 1 kilogram of pure gold or ERC20 tokens. All TOMO are equivalent too, they are the same and have the same value. They are interchangeable 1:1. This is a fungible token.

**Non-fungible tokens (NFTs)** are **all distinct and special**. Every token is rare, with unique atributes and different value. For instance: CryptoKitty tokens, collectible cards, airplane tickets or real art paintings. Every item has its own characteristics and specifics and is clearly differentiable to another one. They are **not interchangeable** 1:1. They are _distinguishable._

> Think of Non-Fungible Tokens (NFT) as a rare collectible on the TomoChain network. Every token has unique characteristics, its own metadata and special attributes

Non-Fungible Tokens (NFT) are used to create verifiable digital scarcity. NFTs are unique and distinctive tokens that you can mainly find on EVM blockchains.

![](<../../.gitbook/assets/image (25).png>)

The [**ERC-721**](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md) is the standard interface for Non-Fungible Tokens (but there are also other NFTs, like ERC1155). ERC721 is a set of rules to make your NFT easy for other people / apps / contracts to interface with.

ERC721 is a free, open standard that describes how to build non-fungible or unique tokens on EVM compatible blockchains. While most tokens are fungible (_not distinguishable_), ERC721 tokens are all unique, with individual identities and properties. Think of them like rare, one-of-a-kind collectables — each unit is a unique item with its own serial number.

> ERC20: identical tokens. ERC721: unique tokens

Some high demand non-fungible tokens are applications like [CryptoKitties](https://www.cryptokitties.co/), [Decentraland](https://decentraland.org/), [CryptoPunks](https://www.larvalabs.com/cryptopunks), and many [others](https://etherscan.io/tokens-nft).

### CryptoKitties <a href="#25ec" id="25ec"></a>

At the end of 2017, NFTs made a remarkable entrance in the blockchain world with the success of **CryptoKitties.** Each one is a unique collectible item, with its own serial number, which can be compared to its DNA card. This unleashed an unprecedented interest for NFTs, that went so far as to clog the Ethereum network. **The CryptoKitties market alone generated $12 million dollars in two weeks after its launch, and over $25 million in total**. Some rare cryptokitties were even [sold for 600 ETH ($170,000)](https://thenextweb.com/hardfork/2018/09/05/most-expensive-cryptokitty/).

**The strength of NFTs resides in the fact that each token is unique and cannot be mistaken for another one**– unlike bitcoins, for example, which are interchangeable with one another.

![](<../../.gitbook/assets/image (60).png>)

### Crypto Item Standard (ERC-1155) <a href="#4a98" id="4a98"></a>

One step further in the non-fungible token space is the ERC-1155 Standard proposed by the [**Enjin team**](https://enjincoin.io/)**,** also known as the “Crypto Item Standard”. This is an improved version of ERC-721 which will actually be suitable for platforms where there are tens of thousands of digital items and goods.

Online games can have up to 100,000 different digital items. The current problem with ERC-721 is that if we would like to tokenize all those 100,000 items, then we would need to deploy 100,000 separate smart contracts.

[ERC-1155 standard](https://blog.enjincoin.io/erc-1155-the-crypto-item-standard-ac9cf1c5a226) combines ERC-20 and ERC-721 tokens in its smart contract. Each token is saved in the contract with a minimal set of data that distinguishes it from others. This allows for the creation of bigger collections which contain multiple different items.

## Use-cases of Non-Fungible Tokens (NFT) <a href="#2194" id="2194"></a>

Most of the time when people think about ERC-721 or NFT, they refer to the most notably successful [CryptoKitties](https://medium.com/u/c8b1419b5d28?source=post\_page-----fe476a68594d----------------------). But there are many other usability applications for NFT contracts:

* **Software titles** or [**software licences**](https://medium.com/collabs-io/software-licences-as-non-fungible-tokens-1f0635913e41) to guarantee anti-piracy, privacy and transferability — like [Collabs.io](https://medium.com/collabs-io)
* **Betting** in real time on the outcome of a video game being live-streamed
* **Gaming** in general is an important field of experimentation and development for the uses of NFT in the future.
* **Concert tickets and sports match tickets** can be tokenized and name-bound, preventing fraud and at the same time offering fans an option to have a single place where to collect all their past event experiences
* **Digital Art** **(or physical art!)** has already entered the game and showed an important usage of ERC721. Digital art auctions were the first application and still are the first thought of non-fungible token standards. The [auctions organized by Christie’s](https://medium.com/cryptokitties/the-ethereal-summit-and-the-140k-cat-a3b561545a44) revealed the appeal of the public for crypto-collectibles. Several digital art assets were sold during this event, the high point being the sale of the ‘Celestial Cyber Dimension’, an ERC721 CryptoKitty piece of art, for [$140,000](https://medium.com/cryptokitties/the-ethereal-summit-and-the-140k-cat-a3b561545a44)
* **Real Estate** assets, to carry out transfers of houses, land and other ‘tokenized’ properties through smart contracts
* **Financial instruments** like loans, burdens and other responsibilities, or a futures contract to buy 1,000 barrels of oil for $60k on May 1
* **KYC compliance** check to verify users. Receiving a specific NFT token in your wallet similar to the _blue checkmark_ ☑️ on Twitter — like [Wyre](https://blog.sendwyre.com/community-driven-on-chain-compliance-d334e0f5962b)
* and more…

[Crypto-Collectibles are more than a passing craze](https://www.disruptordaily.com/why-crypto-collectibles-are-more-than-a-passing-craze/). It is easy to see the reason why, especially when you look at the potential of the crypto-collectible technology, including: **securing digital ownership, protecting intellectual property, tracking digital assets** and overall **creating real world value**.

![](<../../.gitbook/assets/image (33).png>)

## How to deploy a NFT token on TomoChain <a href="#aeea" id="aeea"></a>

This article will create a basic **ERC721** token using the [OpenZeppelin](https://docs.openzeppelin.org/docs/learn-about-tokens.html#erc721) implementation of the [ERC721 standard](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-721.md). Look at the links in order to familiarize yourself with the requirements as they can sometimes be hidden in the excellent [OpenZeppelin ERC721 implementations](https://github.com/OpenZeppelin/openzeppelin-solidity/tree/master/contracts/token/ERC721).

The assets that your ERC721 tokens (NFT) represent will influence some of the design choices for how your contract works, most notably how new tokens are created.

* You can have an initial supply of tokens defined during token creation
* You can have a function, which is only callable by the contract creator (or others — if you allow this) that will issue new tokens when called

For example, in [CryptoKitties](https://www.cryptokitties.co/), players are able to “breed” their Kitties, which creates new Kitties (tokens). However, if your ERC721 token represents something more tangible, like concert tickets, you may not want token holders to be able to create more tokens. In some cases, you may even want token holders to be able to “burn” their tokens, effectively destroying them.

### Let’s Start the NFT Tutorial <a href="#9d55" id="9d55"></a>

We will now implement an NFT collectible token, like CryptoKitties but with simpler logic.

You’ll learn **how to create non fungible tokens**, how to **write tests** for your smart contracts and **how to interact** with them once deployed.

We’ll build non-fungible collectibles: [**gradient tokens**](https://github.com/satansdeer/gradient-token). Every token will be represented as a unique [CSS](https://en.wikipedia.org/wiki/Cascading\_Style\_Sheets) gradient and will look somewhat like this:

## 0. Prerequisites <a href="#46e0" id="46e0"></a>

The first prerequisites you should have:

* Install [**Node.js**](https://nodejs.org/en/download/) & **npm** (“Node.js Package Manager”)
* Install **Truffle**

```
npm install -g truffle
```

## 1. Creating a new project <a href="#42fc" id="42fc"></a>

Create a new directory and move inside it. Then start a new `Truffle`project:

```
mkdir nft-tutorial 
cd nft-tutorial
truffle init
```

We will use [OpenZeppelin ERC721 implementation](https://docs.openzeppelin.org/docs/learn-about-tokens.html#erc721), which is quick and easy and broadly used. Install `OpenZeppelin` in the current folder.

```
npm install openzeppelin-solidity
```

## 2. Preparing your TOMO wallet <a href="#ef52" id="ef52"></a>

[Create a TOMO wallet](../../general/how-to-connect-to-tomochain-network/tomowallet.md). Then grab a few tokens:

* `TomoChain (testnet)`: Get [free tokens from faucet](https://faucet.testnet.tomochain.com/) (grab \~60 TOMO)
* `TomoChain (mainnet)`: You will need real TOMO from exchanges

Go to _Settings_ menu, select _Backup wallet_ and then **Continue**. Here you can see your wallet’s private key and the 12-word recovery phrase.

**Write down your 12-word recovery phrase.**

## 3. Writing the Smart Contract <a href="#ef77" id="ef77"></a>

### 3.1 GradientToken.sol <a href="#bc39" id="bc39"></a>

We’ll be extending the **OpenZeppelin** ERC721 token contracts to create our _Gradient Token_.

1. Go to `contracts/` folder and create a new file called `GradientToken.sol`
2. Copy the following code

```
pragma solidity ^0.5.4;import 'openzeppelin-solidity/contracts/token/ERC721/ERC721Full.sol';
import 'openzeppelin-solidity/contracts/ownership/Ownable.sol';// NFT Gradient token
// Stores two values for every token: outer color and inner colorcontract GradientToken is ERC721Full, Ownable {
  
  using Counters for Counters.Counter;
  Counters.Counter private tokenId;
 
  struct Gradient {
    string outer;
    string inner;
  }
  
  Gradient[] public gradients;  constructor(
    string memory name,
    string memory symbol
  )
    ERC721Full(name, symbol)
    public
  {}
 
 
  // Returns the outer and inner colors of a token 
  function getGradient( uint256 gradientTokenId ) public view returns(string memory outer, string memory inner){
    Gradient memory _gradient = gradients[gradientTokenId];    outer = _gradient.outer;
    inner = _gradient.inner;
  }  // Create a new Gradient token with params: outer and inner
  function mint(string memory _outer, string memory _inner) public payable onlyOwner {
    uint256 gradientTokenId = tokenId.current();
    
    Gradient memory _gradient = Gradient({ outer: _outer, inner: _inner });
    gradients.push(_gradient);
   _mint(msg.sender, gradientTokenId);
    tokenId.increment();
  }
 
}
```

We inherited from two contracts: **ERC721Full** to make it represent a non-fungible token, and from the **Ownable** contract.

Every token will have a **unique** `tokenId`, like a serial number. We also added two attributes: `inner` and `outer` to save CSS colors.

**Ownable** allows managing _authorization_. It assigns ownership to the deployer (when the contract is deployed) and adds _modifier_ **onlyOwner** that allows restrictions to certain methods only to the contract owner. Also, ownership can be transferred. Additionally, third parties can be approved to spend tokens, burn tokens, etc.

Our solidity code is simple and I would recommend a deeper dive into the ERC-721 standard and the OpenZeppelin implementation.

You can see the functions to use in OpenZeppelin ERC721 [here](https://docs.openzeppelin.org/docs/token\_erc721\_erc721) and [here](https://docs.openzeppelin.org/docs/token\_erc721\_erc721token).

You can find another [ERC721 smart contract **example** by OpenZeppelin here](https://docs.openzeppelin.org/docs/learn-about-tokens.html#erc721).

## 4. Config Migrations <a href="#4ff2" id="4ff2"></a>

### 4.1 Create the migration scripts <a href="#18e6" id="18e6"></a>

In the **`migrations/`** directory, create a new file called **`2_deploy_contracts.js`** and copy the following:

```
const GradientToken = artifacts.require("GradientToken");module.exports = function(deployer) {
 
  const _name = "Gradient Token";
  const _symbol = "GRAD";
  
  return deployer
    .then(() => deployer.deploy(GradientToken, _name, _symbol));
};
```

This code will deploy or migrate our contract to TomoChain, with the name `Gradient Token` and the symbol `GRAD`.

### 4.2 Configure truffle.js <a href="#b0d7" id="b0d7"></a>

Now we set up the migrations: the **blockchain** where we want to deploy our smart contract, specify the wallet **address** to deploy, gas, price, etc.

1\. Install Truffle’s `HDWalletProvider`, a separate npm package to find and sign transactions for addresses derived from a 12-word `mnemonic`.

```
npm install truffle-hdwallet-provider
```

2\. Open `truffle.js` file (`truffle-config.js` on Windows). Here the migration settings can be edited: networks, chain IDs, gas... You have multiple networks to migrate your ICO, you can deploy: locally, `ganache`, public `Ropsten (ETH)` testnet, `TomoChain (testnet)`, `TomoChain (Mainnet)`, etc…

Both Testnet and Mainnet **network configurations** are described in [the official TomoChain documentation — Networks.](../working-with-tomochain/) We need the `RPC endpoint`, the `Chain id` and the `HD derivation path`.

Replace the `truffle.js` file with this new content:

```
const HDWalletProvider = require('truffle-hdwallet-provider');
const infuraKey = "a93ffc...<PUT YOUR INFURA-KEY HERE>";// const fs = require('fs');
// const mnemonic = fs.readFileSync(".secret").toString().trim();
const mnemonic = '<PUT YOUR WALLET 12-WORD RECOVERY PHRASE HERE>';module.exports = {  networks: {
    // Useful for testing. The `development` name is special - truffle uses it by default
    development: {
      host: "127.0.0.1",     // Localhost (default: none)
      port: 8545,            // Standard Ethereum port (default: none)
      network_id: "*",       // Any network (default: none)
    },    // Useful for deploying to a public network.
    // NB: It's important to wrap the provider as a function.
    ropsten: {
      //provider: () => new HDWalletProvider(mnemonic, `https://ropsten.infura.io/${infuraKey}`),
      provider: () => new HDWalletProvider(
        mnemonic,
        `https://ropsten.infura.io/${infuraKey}`,
        0,
        1,
        true,
        "m/44'/889'/0'/0/", // Connect with HDPath same as TOMO
      ),
      network_id: 3,       // Ropsten's id
      gas: 5500000,        // Ropsten has a lower block limit than mainnet
      // confirmations: 2,    // # of confs to wait between deployments. (default: 0)
      // timeoutBlocks: 200,  // # of blocks before a deployment times out  (minimum/default: 50)
      // skipDryRun: true     // Skip dry run before migrations? (default: false for public nets )
    },    // Useful for deploying to TomoChain testnet
    tomotestnet: {
      provider: () => new HDWalletProvider(
        mnemonic,
        "https://testnet.tomochain.com",
        0,
        1,
        true,
        "m/44'/889'/0'/0/",
      ),
      network_id: "89",
      gas: 3000000,
      gasPrice: 10000000000000,  // TomoChain requires min 10 TOMO to deploy, to fight spamming attacks
    },    // Useful for deploying to TomoChain mainnet
    tomomainnet: {
      provider: () => new HDWalletProvider(
        mnemonic,
        "https://rpc.tomochain.com",
        0,
        1,
        true,
        "m/44'/889'/0'/0/",
      ),
      network_id: "88",
      gas: 3000000,
      gasPrice: 10000000000000,  // TomoChain requires min 10 TOMO to deploy, to fight spamming attacks
    },    // Useful for private networks
    // private: {
      // provider: () => new HDWalletProvider(mnemonic, `https://network.io`),
      // network_id: 2111,   // This network is yours, in the cloud.
      // production: true    // Treats this network as if it was a public net. (default: false)
    // }
  },  // Set default mocha options here, use special reporters etc.
  mocha: {
    // timeout: 100000
  },  // Configure your compilers
  compilers: {
    solc: {
      version: "0.5.4",    // Fetch exact version from solc-bin (default: truffle's version)
      // docker: true,        // Use "0.5.1" you've installed locally with docker (default: false)
      // settings: {          // See the solidity docs for advice about optimization and evmVersion
      //  optimizer: {
      //    enabled: false,
      //    runs: 200
      //  },
      //  evmVersion: "byzantium"
      // }
    }
  }
}
```

3\. Remember to **update the `truffle.js` file using your own wallet recovery phrase.** Copy the 12 words previously obtained from your wallet and paste it as the value of the `mnemonic` variable.

```
const mnemonic = '<PUT YOUR WALLET 12-WORD RECOVERY PHRASE HERE>';
```

> **⚠️ Warning**: In production, it is highly recommend storing the _`mnemonic`_ in another secret file (loaded from environment variables or a secure secret management system)...

### 4.3 Ganache <a href="#a349" id="a349"></a>

You can use `Ganache` blockchain to test your smart contracts locally, before migrating to a public blockchain like `Ethereum (Ropsten)` or `Tomochain`.

On a separate console window, install `Ganache` and run it:

```
npm install -g ganache-cli
ganache-cli -p 8545
```

`Ganache` will start running, listening on port `8545`. Automatically you will have 10 available wallets with their private keys and `100 ETH` each. You can use them to test your smart contracts.

![](<../../.gitbook/assets/image (4).png>)

## 5. Adding Tests <a href="#9c8f" id="9c8f"></a>

We will add now tests to check our smart contracts.

When deploying contracts the first contract will usually be the deployer. This test will check that.

Create `GradientTokenTest.js` in `/test` directory and write the following test:

```
const GradientToken = artifacts.require("GradientToken");contract("Gradient token", accounts => {
  it("Should make first account an owner", async () => {
    let instance = await GradientToken.deployed();
    let owner = await instance.owner();
    assert.equal(owner, accounts[0]);
  });
});
```

Here we run the `contract` block, that deploys our contract. We wait for the contract to be deployed and request `owner()` which returns owner’s address. Then we **assert** that the **owner address is the same as `account[0]`**.

> **Note:** Make sure that `Ganache` is running (on a different console).

Run the test:

```
truffle test
```

![](<../../.gitbook/assets/image (43).png>)

The test should **pass**. This means that the smart contract **works correctly** and it did successfully what it was expected to do.

### Adding more tests <a href="#1f31" id="1f31"></a>

Every NFT token will have a unique ID. The first minted token has `ID: 0`, the second one has `ID: 1`, and on and on…

Now we’ll test the `mint` function. Add the following test:

```
describe("mint", () => {
  it("creates token with specified outer and inner colors", async () => {
    let instance = await GradientToken.deployed();
    let owner = await instance.owner();    let token0 = await instance.mint("#ff00dd", "#ddddff");
    let token1 = await instance.mint("#111111", "#ffff22");
    let token2 = await instance.mint("#00ff00", "#ffff00");    let gradients1 = await instance.getGradient( 1 );
    assert.equal(gradients1.outer, "#111111");
    assert.equal(gradients1.inner, "#ffff22");
  });
});
```

This test is simple. First we check that we can mint new tokens. We mint 3 tokens. Then we expect that the unique attributes `outer` and `inner` of token with **tokenId = `1`** are saved correctly and we assert it by using the `getGradient` function that we created before.

The test passed.

![](<../../.gitbook/assets/image (45).png>)

## 6. Deploying <a href="#e1b9" id="e1b9"></a>

### 6.1 Start the migration <a href="#c886" id="c886"></a>

You should have your smart contract already compiled. Otherwise, now it’s a good time to do it with `truffle compile`.

> **Note:** Check that you have enough _`TOMO`_ tokens in your wallet!! I recommend at least **`60 TOMO`** to deploy this smart contract

Back in our terminal, migrate the contract to **TomoChain testnet** network:

```
truffle migrate --network tomotestnet
```

To deploy to the **TomoChain mainnet** is very similar:

```
truffle migrate --network tomomainnet
```

The migrations start…

```
Starting migrations...
======================
> Network name:    'tomotestnet'
> Network id:      89
> Block gas limit: 840000001_initial_migration.js
======================Deploying 'Migrations'
   ----------------------
   > transaction hash:    0x67c0f12247d0bb0add43e81e8ad534df9cd7d3473ef76f5b60cee3e3d34bae1a
   > Blocks: 2            Seconds: 5
   > contract address:    0x6056dC38715C7d2703a8aA94ee68A964eaE86fdc
   > account:             0x169397F515Af9E93539e0F483f8A6FC115de660C
   > balance:             90.05683
   > gas used:            273162
   > gas price:           10000 gwei
   > value sent:          0 ETH
   > total cost:          2.73162 ETH> Saving artifacts
   -------------------------------------
   > Total cost:             2.73162 ETH2_deploy_contracts.js
=====================Deploying 'GradientToken'
   -------------------------
   > transaction hash:    0xca09a87ad8f834644dcb85f8ea89beff74b818eff11d355e0774e6b60c51718c
   > Blocks: 2            Seconds: 5
   > contract address:    0x8B830F38b798B7b39808A059179f2c228209514C
   > account:             0x169397F515Af9E93539e0F483f8A6FC115de660C
   > balance:             60.64511
   > gas used:            2941172
   > gas price:           10000 gwei
   > value sent:          0 ETH
   > total cost:          29.41172 ETH> Saving artifacts
   -------------------------------------
   > Total cost:            29.41172 ETHSummary
=======
> Total deployments:   2
> Final cost:          32.14334 ETH
```

**Congratulations!** You have already deployed your non-fungible token (NFT) to TomoChain! The deployment fees were `32.14 TOMO`.

Read the output text on the screen. The NFT token [contract address](https://scan.testnet.tomochain.com/address/0x8B830F38b798B7b39808A059179f2c228209514C) is _(yours will be different)_:

```
0x8B830F38b798B7b39808A059179f2c228209514C
```

> **⚠️ Note:** TomoChain’s smart contract[ **creation fee**](../working-with-tomochain/)**:** gas price 10000 Gwei, gas limit >= 1000000

### \*\*\* Troubleshooting \*\*\* <a href="#f097" id="f097"></a>

* **Error: `smart contract creation cost is under allowance`**. \*\*Why?\*\*Increasing transaction fees for smart contract creation is one of the ways TomoChain offers to defend against spamming attacks. **Solution:** edit `truffle.js` and add more gas/gasPrice to deploy.
* **Error: `insufficient funds for gas * price + value`. Why?** You don’t have enough tokens in your wallet for gas fees. **Solution:** you need more funds in your wallet to deploy, go to [faucet](https://faucet.testnet.tomochain.com/) and get more tokens.

## **7. Interacting with the smart contract** <a href="#4ecf" id="4ecf"></a>

### **7.1 Minting new Tokens** <a href="#ad83" id="ad83"></a>

Now to create a new Gradient Token you can call:

```
GradientToken(gradientTokenAddress).mint("#001111", "#002222")
```

You can call this function [via MyEtherWallet/Metamask or Web3](https://medium.com/@blockchain101/interacting-with-deployed-ethereum-contracts-in-truffle-39d7c7040455)... In a Dapp or game this would probably be called from a button click in a UI.

Let’s use [MyEtherWallet](https://www.myetherwallet.com/interface/interact-with-contract) (MEW) to interact with the contract. We use [MetaMask](https://metamask.io/) to connect to the GradientToken **owner** **wallet** in TomoChain (testnet), then we will call function `mint()` to mint the first token.

![](<../../.gitbook/assets/image (38) (1).png>)

In MyEtherWallet, under menu `Contract` > `Interact with Contract` two things are required:

* **Contract Address:** you got this address when you deployed
* **ABI:** file `build/contracts/GradientToken.json`, search `"abi": [` … `]`and copy everything inside brackets, including brackets. Then paste on MEW

On the right you will see a dropdown list with the functions. Select `mint`. MEW will show two fields: `outer` and `inner`. Input two colors, like `#ff0000`or `#0000ff` and click the button **Write**. Confirm with **MetaMask**.

![](<../../.gitbook/assets/image (11).png>)

Here is [our contract address](https://scan.testnet.tomochain.com/address/0x8B830F38b798B7b39808A059179f2c228209514C), and the new `mint` transaction:

![](<../../.gitbook/assets/image-2-copy (2).png>)

You can use MEW to _**Write**_ and to _**Read**_ functions, like `getGradient`! This way you can check if values are correct, totalSupply, transfer tokens...

{% hint style="info" %}
In `Ethereum (Ropsten)`, the Etherscan page with [our migrated contract](https://ropsten.etherscan.io/address/0x22fb8a49811d33d34be96c82b3937b252e78a8d5) will **change** after the first token is minted. A new link will be displayed now to track the ERC721 token `GRAD`.
{% endhint %}

![](<../../.gitbook/assets/image (8).png>)

![](<../../.gitbook/assets/image (1).png>)

## What’s next? <a href="#2883" id="2883"></a>

A few suggestions to continue from here:

* You could add a lot of different attributes to your unique NFT tokens
* You can [connect to a JS front end](https://maksimivanov.com/posts/gradient-coin-tutorial-part-3) and show your tokens
* You can have some buttons to interact with the tokens (buy, sell, change, transfer, change attributes/colors, etc…)
* You can iterate on this basic code and create a new **CryptoKitties** game :)

![](<../../.gitbook/assets/image (16).png>)

**Congratulations!** You have learned about non-fungible tokens, use-cases of NFTs and how to deploy NFT tokens on TomoChain.

### Source Code <a href="#04a2" id="04a2"></a>

The source code for this tutorial is available on [Github](https://github.com/DuqueKarl/NFTGradientToken).
