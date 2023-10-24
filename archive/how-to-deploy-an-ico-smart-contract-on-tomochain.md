---
description: Creating a TRC20 Token Crowdsale with Truffle and OpenZeppelin
---

# How to deploy an ICO smart contract on TomoChain

This article will go through the process of **creating a basic ICO on TomoChain** using TRC20 tokens issued on TomoChain.

![](<../.gitbook/assets/image-2-copy (1).png>)

In this tutorial we will be covering:

* What is an **ICO**?
* Some important concepts such as TRC20, total supply, whitelist, ...
* Using **Truffle** framework and **OpenZeppelin** code framework
* Writing a **TRC20 token** (TomoChain) smart contract
* Writing a **Crowdsale** smart contract
* **Deploying your ICO** smart contract to **TomoChain testnet** or Ethereum/Ropsten (it is totally compatible!)
* **Buying** the new ICO tokens

An **ICO (Initial Coin Offering)** is a new way to raise funds for startups. It is the cryptocurrency equivalent to an IPO in the mainstream investment world. A company looking to create a new coin, app, or service launches an ICO. Investors buy the new ICO token, normally with preexisting digital tokens like TOMO. The company holding the ICO uses the investor funds as a means of furthering its goals, launching its product, or starting its digital currency. ICO rounds are similar to venture capitalists (VC) rounds.

**Tokens** are essentially smart contracts that make use of the TomoChain blockchain. The **TRC20** **token standard** defines a common list of rules for all TomoChain tokens to follow, similar to the ERC20 standard in Ethereum.

In the **smart contract** you can setup general token specifics like the **rate** of TOMO per token (the number of tokens the user gets for his TOMO which may change with time), the ICO **start** and **finish date**, time-line **bonuses**…

The **total supply** is the total amount of tokens that will exist. For instance, TomoChain’s total supply is 100 million tokens, but currently there are only 58–60 million tokens _**in circulation**_. The remaining tokens are locked for different purposes like team reserves, partnerships, masternode and staking rewards, community rewards and more, and will enter in circulation over the next years.

ICOs can have one or multiple **rounds**. For instance, a **PreSale** round for private investors with some bonus, and later a public **Crowdsale**.

Some ICOs use a **whitelist**. This means that participants have to **register in advance to participate in the ICO** sale. Whitelists usually limit the number of spots and/or the initial min/max buy. Investors may need to register with some documents, to comply with some countries regulations, KYC/AML…

Besides the law, take into account the **security** issue for the smart contracts and try to make contracts as simple as possible (security loves simple).

> The idea of a crowdsale, ICO, or a token sale is simple. You can automate exchanging your tokens for the base cryptocurrency (like ETH or TOMO), and you do it with a smart contract

The **smart contract** that we use in this tutorial is very simple and only for educational purposes. In fact, the scenario for an ICO is more complicated and needs to be tested and audited to prevent bugs. Finally, compliance with the laws and regulations of the country where the ICO is conducted should be adhered to.

**This tutorial will walk through the steps of setting up an account through issuing an ICO contract on TomoChain network using simple smart contracts and MetaMask.**

For this tutorial we are using:

* [**Truffle**](https://truffleframework.com/), a world class development environment, testing framework and asset pipeline for blockchains using the Ethereum Virtual Machine (EVM), aiming to make life as a developer easier.
* [**OpenZeppelin**](https://openzeppelin.org/), a battle-tested framework of reusable smart contracts for Ethereum and other EVM blockchains.

### Steps to Follow (Overview) <a href="#5c6b" id="5c6b"></a>

1. Write Solidity smart contracts
2. Deploy locally (local Eth node/Ganache/Ropsten/etc) and test it
3. Deploy to TomoChain TestNet and test it
4. Deploy to TomoChain MainNet

## 0. Prerequisites <a href="#c774" id="c774"></a>

To start building your ICO smart contract you will need:

* Install [**Node.js**](https://nodejs.org/en/download/) & **npm** (“Node.js Package Manager”)
* Install **Truffle**

```
npm install -g truffle
```

## 1. Creating a new project <a href="#64ed" id="64ed"></a>

Create a new directory in your development folder of choice and then move inside it. Then start a new `Truffle` project:

```
mkdir trc20-crowdsale-tutorial 
cd trc20-crowdsale-tutorial
truffle init
```

Now we install `OpenZeppelin` in this folder:

```
npm install openzeppelin-solidity
```

## 2. Preparing your TOMO wallet <a href="#ef52" id="ef52"></a>

**You will need a wallet address** and some tokens. We will show how to do it on both TomoChain Testnet and Mainnet.

### 2.1 Create a TOMO wallet and save the Mnemonic <a href="#eb9e" id="eb9e"></a>

Create a new TOMO wallet using **TomoWallet** mobile app for [iOS](https://itunes.apple.com/us/app/tomo-wallet/id1436476145?mt=8) or [the web version](https://wallet.tomochain.com/#/login). Under _Settings_ go to _Advanced Settings._ Here _Choose network_ and select `TomoChain TestNet` or `TomoChain` \[mainnet].

Go to the _Settings_ menu, select _Backup wallet_ and then **Continue**. Here you can see your wallet’s private key and the 12-word recovery phrase. **Write down the 12-word recovery phrase.**

You can also create a new [TomoChain wallet with MetaMask, MyEtherWallet or TrustWallet](../general/how-to-connect-to-tomochain-network/). For instance, for mainnet go to [MyEtherWallet](https://www.myetherwallet.com/) and select **TOMO (tomochain.com)** instead of Ethereum. Enter a password and then Create a new wallet. **Write down your recovery phrase.**

For this tutorial, my wallet address (testnet) is:

```
0xc9b694877acd4e2e100e095788a591249c38b9c5
```

My recovery phrase (12-word `mnemonic`) is:

```
myth ahead spin horn minute tag spirit ... camera
```

Write them down. This will be needed later. **Notice that your wallet address and your recovery phrase will be different than mine.**

> **⚠️ Important!** Always keep your private key and recovery phrase **secret!**

### 2.2 Get some TOMO funds <a href="#2e01" id="2e01"></a>

We will need some tokens for smart contract deployment and also to test later with our ICO smart contracts.

**Testnet:** Receive 15 free testnet TOMO tokens using [TomoChain’s Faucet](https://faucet.testnet.tomochain.com/).

**Mainnet:** You need real TOMO tokens from exchanges.

Go to faucet and collect `60 TOMO`. Now your wallet has enough balance to do everything in this tutorial so… let’s go ahead!

### 2.3 The Block Explorer <a href="#07a6" id="07a6"></a>

To check the balance of a wallet address, use **TomoScan**.

**Testnet:** [https://testnet.tomoscan.io/](https://testnet.tomoscan.io/)

**Mainnet:** [https://tomoscan.io/](https://tomoscan.io/)

> **Note:** Create 2 different TOMO wallets, both with some tokens. The first wallet is to deploy the ICO smart contract or `deployment wallet`, the second one will be used to test it or `buyer wallet`.

## 3. Writing the Smart Contracts <a href="#7bd0" id="7bd0"></a>

### 3.1 MyToken <a href="#bc39" id="bc39"></a>

We use and extend **OpenZeppelin** contracts to create more secure Dapps in less time. OpenZeppelin comes with a wide array of smart contracts for various important functions.

We’ll be extending now the token contracts to create our own [ERC20](https://theethereum.wiki/w/index.php/ERC20\_Token\_Standard)-compliant (TRC20) token.

1. Go to `contracts/` directory and create a new file called `MyToken.sol` or the name you like.
2. Copy the following code

```
pragma solidity ^0.5.2;import "openzeppelin-solidity/contracts/token/ERC20/ERC20.sol";
import "openzeppelin-solidity/contracts/token/ERC20/ERC20Detailed.sol";
import "openzeppelin-solidity/contracts/ownership/Ownable.sol";/**
 * @title ERC20Detailed token
 * @dev The decimals are only for visualization purposes.
 * All the operations are done using the smallest and indivisible token unit,
 * just as on Ethereum all the operations are done in wei.
 */
contract MyToken is ERC20, ERC20Detailed, Ownable {
  
  constructor(
    string memory _name,
    string memory _symbol,
    uint8 _decimals,
    uint256 _initialSupply
  ) 
    ERC20Detailed(_name, _symbol, _decimals)
    public
  {
    _mint(msg.sender, _initialSupply * 10 ** uint256(_decimals));
  }}
```

That’s all. Really.

Hold on a minute… Are you telling me that **this is the full code of an ERC20 / TRC20 token**? Exactly. This is the beauty of inheritance and extending OpenZeppelin smart contracts. Currently, see the first few lines? All the code included in `openzeppelin-solidity/contracts/token/ERC20/ERC20.sol` and `openzeppelin-solidity/contracts/token/ERC20/ERC20Detailed` can be used and extended (update/overwrite) by this token.

We’re extending `ERC20`, `ERC20Detailed` and `Ownable` smart contracts, by OpenZeppelin. This means that we will have all the functionality of those smart contracts plus the code we add to our file `MyToken.sol`.

This code will initialize the token values like `name`, `symbol`, `decimals` (we do this using `ERC20Detailed`). With the `_mint()` instruction we are pre-minting (creating) all the `initialSupply` (the total amount of tokens that will be created). All the tokens will be sent to the wallet address of the `MyToken` contract. We give the entire supply to the deploying account’s address.

```
_mint(msg.sender, _initialSupply * 10 ** uint256(_decimals));
```

> ⚠️ **Important:** All currency math is done in the smallest unit of that currency, which is not ETH (or TOMO) but **wei**. `1 ETH = 10¹⁸ wei`

Later, we will grant access to these funds to the `MyTokenCrowdsale` smart contract. To transfer ownership or **approve** another wallet accesing our smart contract funds, we inherited the `Ownable` smart contract.

### 3.2 MyTokenCrowdsale <a href="#4dbf" id="4dbf"></a>

Now we are going to write our Crowdsale smart contract.

1. In the `contracts/` folder, add a new file called `MyTokenCrowdsale` (or the name you like).
2. Open the file and paste this code:

```
pragma solidity ^0.5.2;import "openzeppelin-solidity/contracts/token/ERC20/ERC20.sol";
import "openzeppelin-solidity/contracts/crowdsale/Crowdsale.sol";
import "openzeppelin-solidity/contracts/crowdsale/emission/AllowanceCrowdsale.sol";contract MyTokenCrowdsale is Crowdsale, AllowanceCrowdsale {  constructor(
    uint256 _rate,
    address payable _wallet,
    ERC20 _token,
    address _tokenWallet
  )
    Crowdsale(_rate, _wallet, _token)
    AllowanceCrowdsale(_tokenWallet)
    public
  {  }
}
```

Again, very simple smart contract.

We extended OpenZeppelin’s basic `Crowdsale` and `AllowanceCrowdsale`. Crowdsale works with `rate`, `wallet` (the address of MyTokenCrowdsale contract), `token` (the TRC20 token).

We extended **AllowanceCrowdsale** so this contract will be able to access and send tokens stored in another wallet, **once approved by the owner of the tokens** — which is `MyToken`.

## 4. Config Migrations <a href="#8bdf" id="8bdf"></a>

### 4.1 Create the migration scripts <a href="#18e6" id="18e6"></a>

In the **`migrations/`** directory, create a new file called\*\*`2_deploy_contracts.js`\*\*and add the following content:

```
const MyToken = artifacts.require("./MyToken.sol");
const MyTokenCrowdsale = artifacts.require("./MyTokenCrowdsale.sol");const web3 = require("web3-utils");module.exports = (deployer, network, [owner]) => {  const _name = "My Token TRC20";
  const _symbol = "MYT";
  const _decimals = 18;
  const _initialSupply = 16000000;
  const _rate = 500;
  const _crowdsaleTokens = web3.toWei("8000000", "ether");
   
  return deployer
    .then(() => deployer.deploy(MyToken, _name, _symbol, _decimals, _initialSupply))
    .then(() => deployer.deploy(MyTokenCrowdsale, _rate, owner, MyToken.address, owner))
    .then(() => MyToken.deployed())
    .then(token => token.approve(MyTokenCrowdsale.address, _crowdsaleTokens ));
};
```

We are going to explain briefly what is happening here:

We have selected the name of our token: `My Token TRC20`. We have chosen the symbol `MYT` for this token. We assign `18 decimals` which is standard.

We are also going to create the initial supply: `16'000'000` tokens. But **we will only sell half (50%)** of them in the Crowdsale.

We first deploy `MyToken`, creating the initial supply: `16'000'000 MYT`. Then we deploy `MyTokenCrowdsale`. Next, we tell `MyToken` to `approve` the `MyTokenCrowdsale` address to access `8'000'000 MYT`. This is the max that we will sell in our Crowdsale.

**One more thing**. For this to work, we need to install `web3-utils`. We use this for big numbers like `web3.toWei()` function, because we need `8'000'000` followed by 18 zeros. Just execute this on the console:

```
npm install web3-utils
```

### 4.2 Configure truffle.js <a href="#0f37" id="0f37"></a>

Before starting the migration, we need to specify the **blockchain** where we want to deploy our smart contracts, specify the **address** to deploy — the wallet we just created, and optionally the gas, gas price, etc.

1\. Install Truffle’s `HDWalletProvider`, a separate npm package to find and sign transactions for addresses derived from a 12-word `mnemonic`.

```
npm install truffle-hdwallet-provider
```

2\. Open `truffle.js` file (`truffle-config.js` on Windows). You can edit here the migration settings: networks, chain IDs, gas... You have multiple networks to migrate your ICO, you can deploy: locally, to `ganache`, to public `Ropsten (ETH)` testnet, to `TomoChain (testnet)`, to `TomoChain (Mainnet)`, etc…

[The official TomoChain documentation — Networks](../developer-guide/working-with-tomochain/) is very handy. Both Testnet and Mainnet **network configurations** are described there. We need the `RPC endpoint`, the `Chain id` and the `HD derivation path`.

Replace the `truffle.js` file with this new content:

```
/**
 * Use this file to configure your truffle project. It's seeded with some
 * common settings for different networks and features like migrations,
 * compilation and testing. Uncomment the ones you need or modify
 * them to suit your project as necessary.
 *
 * More information about configuration can be found at:
 *
 * truffleframework.com/docs/advanced/configuration
 *
 * To deploy via Infura you'll need a wallet provider (like truffle-hdwallet-provider)
 * to sign your transactions before they're sent to a remote public node. Infura API
 * keys are available for free at: infura.io/register
 *
 * You'll also need a mnemonic - the twelve word phrase the wallet uses to generate
 * public/private key pairs. If you're publishing your code to GitHub make sure you load this
 * phrase from a file you've .gitignored so it doesn't accidentally become public.
 *
 */const HDWalletProvider = require('truffle-hdwallet-provider');
const infuraKey = "a93ffc...<PUT YOUR INFURA-KEY HERE>";// const fs = require('fs');
// const mnemonic = fs.readFileSync(".secret").toString().trim();
const mnemonic = '<PUT YOUR WALLET 12-WORD RECOVERY PHRASE HERE>';module.exports = {
  /**
   * Networks define how you connect to your ethereum client and let you set the
   * defaults web3 uses to send transactions. If you don't specify one truffle
   * will spin up a development blockchain for you on port 9545 when you
   * run `develop` or `test`. You can ask a truffle command to use a specific
   * network from the command line, e.g
   *
   * $ truffle test --network <network-name>
   */  networks: {
    // Useful for testing. The `development` name is special - truffle uses it by default
    // if it's defined here and no other network is specified at the command line.
    // You should run a client (like ganache-cli, geth or parity) in a separate terminal
    // tab if you use this network and you must also set the `host`, `port` and `network_id`
    // options below to some value.
    
    development: {
      host: "127.0.0.1",     // Localhost (default: none)
      port: 8545,            // Standard Ethereum port (default: none)
      network_id: "*",       // Any network (default: none)
    },    // Another network with more advanced options...
    // advanced: {
      // port: 8777,             // Custom port
      // network_id: 1342,       // Custom network
      // gas: 8500000,           // Gas sent with each transaction (default: ~6700000)
      // gasPrice: 20000000000,  // 20 gwei (in wei) (default: 100 gwei)
      // from: <address>,        // Account to send txs from (default: accounts[0])
      // websockets: true        // Enable EventEmitter interface for web3 (default: false)
    // },    // Useful for deploying to a public network.
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
      gas: 2000000,
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
      gas: 2000000,
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
      version: "0.5.2",    // Fetch exact version from solc-bin (default: truffle's version)
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

3\. Remember to **update the `truffle.js` file using your own wallet recovery phrase.** Copy the 12 words obtained previously and paste it as the value of the `mnemonic` variable.

```
const mnemonic = '<PUT YOUR WALLET 12-WORD RECOVERY PHRASE HERE>';
```

If you want to use `Ropsten` (Ethereum) to deploy, you should update your `infuraKey`. Otherwise you can ignore this line:

```
const infuraKey = "a93ffc...<PUT YOUR INFURA-KEY HERE>";
```

> Our Solidity code works perfectly on Ethereum (deploying to `Ropsten`) and the exact same code works too on `TomoChain`. — Nice! Totally compatible!

> **⚠️ Warning**: In production, we highly recommend storing the `mnemonic` in another secret file (loaded from environment variables or a secure secret management system), to reduce the risk of the mnemonic becoming known. If someone knows your mnemonic, they have all of your addresses and private keys!

_Also, the use of environment variable for mnemonics is a good practice if multiple developers work on the same code stored on a remote repo and they can use their different mnemonics to test/deploy the contract._

_You can try with npm package `dotenv` to load an environment variable from an `.env` file, — then update your truffle.js to use this secret `mnemonic`._

## **5. Deploying** <a href="#e1b9" id="e1b9"></a>

### 5.1 Start the migration <a href="#c886" id="c886"></a>

You should have your smart contract already compiled. Otherwise, now it’s a good time to do it with `truffle compile`.

Back in our terminal, migrate the contract to **TomoChain testnet** network (remember that you need some testnet `TOMO` on your wallet):

```
truffle migrate --network tomotestnet
```

To deploy to **TomoChain mainnet** is very similar:

```
truffle migrate --network tomomainnet 
```

You could also migrate the contract to **Ropsten** (but first you need a Ropsten wallet with some `Ropsten ETH` - _you can do this on `Metamask`_ [_with faucet_](https://faucet.metamask.io/)).

```
truffle migrate --network ropsten 
```

> Deployment is waaay faster on TomoChain!

The migrations start…

```
Starting migrations...
======================
> Network name:    'tomotestnet'
> Network id:      89
> Block gas limit: 840000001_initial_migration.js
======================Deploying 'Migrations'
   ----------------------
   > transaction hash:    0xb04b1a80cfedbcb8248817301c0c9384ee41099a4c25266a61cae87c76cafc05
   > Blocks: 2            Seconds: 5
   > contract address:    0xf227316d891D0D83a04d5C6EE0A745585DdAE1a7
   > account:             0x169397F515Af9E93539e0F483f8A6FC115de660C
   > balance:             46.26451
   > gas used:            273162
   > gas price:           10000 gwei
   > value sent:          0 ETH
   > total cost:          2.73162 ETH> Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:             2.73162 ETH2_deploy_contracts.js
=====================Deploying 'MyToken'
   -------------------
   > transaction hash:    0xd084fcd12c9e05397abfffc78e680a2415f061d0d36d3a13ac416b798f4d0f19
   > Blocks: 0            Seconds: 0
   > contract address:    0xd2e70E8386C9E3DeCA6583686a12F8da62b59969
   > account:             0x169397F515Af9E93539e0F483f8A6FC115de660C
   > balance:             29.38373
   > gas used:            1646050
   > gas price:           10000 gwei
   > value sent:          0 ETH
   > total cost:          16.4605 ETHDeploying 'MyTokenCrowdsale'
   ----------------------------
   > transaction hash:    0x3f375af43846307544d7d7652994f2bb9264a743aa064f7b8c1c92e68530502c
   > Blocks: 0            Seconds: 0
   > contract address:    0xD102e777e893f30cb9630a32A9370ED6d575226B
   > account:             0x169397F515Af9E93539e0F483f8A6FC115de660C
   > balance:             21.24818
   > gas used:            813555
   > gas price:           10000 gwei
   > value sent:          0 ETH
   > total cost:          8.13555 ETH> Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:            24.59605 ETHSummary
=======
> Total deployments:   3
> Final cost:          27.32767 ETH
```

**Congratulations!** You have already deployed your ICO smart contracts to TomoChain. The deployment fees have costed `27.32 TOMO`.

Read carefully and **write down** the output text on the screen:

* `MyToken` contract address is:

```
0xd2e70E8386C9E3DeCA6583686a12F8da62b59969
```

* `MyTokenCrowdsale` contract address is:

```
0x169397F515Af9E93539e0F483f8A6FC115de660C
```

### \*\*\* Troubleshooting \*\*\* <a href="#f097" id="f097"></a>

* **Error: `smart contract creation cost is under allowance`**. **Why?** Increasing transaction fees for smart contract creation is one of the ways TomoChain offers to defend against spamming attacks. **Solution:** edit `truffle.js` and add more gas/gasPrice to deploy.
* **Error: `insufficient funds for gas * price + value`. Why?** You don’t have enough tokens in your wallet for gas fees. **Solution:** you need more funds in your wallet to deploy, go to [faucet](https://faucet.testnet.tomochain.com/) and get more tokens.

### 5.3 Check the deployment contracts <a href="#10d5" id="10d5"></a>

If you want to verify that your contracts were deployed successfully, you can check on **TomoScan** [testnet](https://testnet.tomoscan.io/) (or [mainnet](https://tomoscan.io/)). In the search field, type in the contract address you want to see.

Here are the results of our migrations:

**Ropsten:**

* Token: [0x1679808c30FE76bA30AD9D8AdCDff92f67aa8f3B](https://ropsten.etherscan.io/token/0x1679808c30fe76ba30ad9d8adcdff92f67aa8f3b)
* Crowdsale: [0xe38C915d87b22FBafb72CE8c39Da8d0c57284c90](https://ropsten.etherscan.io/address/0xe38C915d87b22FBafb72CE8c39Da8d0c57284c90)

**TomoChain testnet:**

* Token: [0xd2e70e8386c9e3deca6583686a12f8da62b59969](https://testnet.tomoscan.io/address/0xd2e70e8386c9e3deca6583686a12f8da62b59969)
* Crowdsale: [0xD102e777e893f30cb9630a32A9370ED6d575226B](https://scan.testnet.tomochain.com/address/0xD102e777e893f30cb9630a32A9370ED6d575226B)

![](<../.gitbook/assets/image-2-copy (3).png>)

**Congratulations!** You’ve deployed **your ICO smart contract and TRC20 token to TomoChain using Truffle and OpenZeppelin.** It’s time to interact now with our ICO smart contract to make sure it does what we want.

## 6. Testing the smart contracts <a href="#e3e1" id="e3e1"></a>

The code used in this tutorial is just for **learning purposes.** When writing your ICO contracts take time to **test and audit your own code**, writing unit tests on `test/` folder and auditing your code to prevent bugs or hacks.

## 7. Testing the ICO <a href="#b472" id="b472"></a>

The last step is testing our ICO. We will **buy** some `MYT` tokens with `TOMO`!

For this, we will **directly send some `TOMO` tokens to the Crowdsale contract address**, and the smart contract must send back the new TRC20 token we created, `MYT`.

The conversion rate is `500`. So, if we send `20 TOMO` we should receive `20 * 500 = 10'000 MYT` in our buyer wallet.

### 7.1 Install MetaMask <a href="#77e6" id="77e6"></a>

1. Install the [MetaMask browser extension](https://metamask.io/) in Chrome or FireFox.
2. Once installed, you’ll see the MetaMask fox icon next to your address bar. Click the icon and MetaMask will open up.
3. Create a New password. Then, write down the Secret Backup Phrase and accept the terms. By default, MetaMask will create a new Ethereum address for you.

![](<../.gitbook/assets/image (14).png>)

4\. Now we’re connected to the Ethereum network,with a brand new wallet.

### 7.2 Config MetaMask to connect to TomoChain <a href="#d049" id="d049"></a>

Let’s now connect MetaMask to `TomoChain (testnet)`.

1\. Click the menu with the “Main Ethereum Network” and select **Custom RPC**. Use the [Networks data from TomoChain](../developer-guide/working-with-tomochain/) (testnet) and click **Save**.

![](<../.gitbook/assets/image (15).png>)

2\. The network name at the top will switch to say “TomoChain testnet”. Now that we are on TomoChain network we can import TomoChain wallets.

> Don’t use the `deployment wallet` you previously used on `truffle.js`. Better, **create a new TOMO wallet**, to separate roles. Create your `buyer wallet`, if you haven’t already, then go to faucet and add `30 TOMO`.

3\. **Copy the private key of your `buyer wallet`**. Back to MetaMask, click on the top-right circle and select **Import Account.** Paste the private key and _voilà_! Your TOMO wallet is loaded in MetaMask.

![](<../.gitbook/assets/image (70).png>)

### 7.3 Buying ICO tokens (sending TOMO to the ICO address) <a href="#9432" id="9432"></a>

We will now buy some `MyToken (MYT)` from the ICO Crowdsale contract.

1\. Copy the Crowdsale contract `address`. Here is the address in our example (your Crowdsale address will be different)

```
0xD102e777e893f30cb9630a32A9370ED6d575226B
```

2\. Go to **MetaMask**, connecting to `TomoChain testnet` and using your _buyer wallet_ with enough funds. Click the **Send** button.

3\. Paste the `Crowdsale address`. Set the amount `20 TOMO` you want to send. Select the **Transaction Fee** (gas, gas price) and click **Next**. After a few seconds your transaction will be confirmed as successful.

![](<../.gitbook/assets/image (9) (1).png>)

You can see the Crowdsale buy transaction. `20 TOMO` were sent, and the contract sent `10'000 MYT` back to the buyer wallet. [Here is the transaction](https://scan.testnet.tomochain.com/txs/0xc35a3d487ca0a87b85b6c113ae7776ab70eb8ee3310490c772dc68cf830191ec) of this tutorial on **TomoScan**.

Now you can visit the [Token Holders list](https://scan.testnet.tomochain.com/tokens/0xd2e70e8386c9e3deca6583686a12f8da62b59969#tokenHolders), and you will find two holders:

* The ICO/team: has `15'990'000 MYT`
* Our buyer wallet: has `10'000 MYT`

![](<../.gitbook/assets/image (68).png>)

To see your new tokens on MetaMask, click the **Menu** icon on top left (below the Fox face). Click **Add Token**. Select **Custom Token**, paste the token address and hit **Next**.

You will see your `MYT` tokens.

![](<../.gitbook/assets/image (40).png>)

**Congratulations!** The Crowdsale is working! We sent `20 TOMO` and we got back `10'000 MYT`.

## What’s next? <a href="#b362" id="b362"></a>

You can and should customize these two smart contracts `MyToken` and `MyTokenCrowdsale` according to your needs. For instance, you can:

* add an `openingTime` and `closingTime` to your crowdsale
* set a different `rate` or bonuses with dates (example: `rate: 600` during the first week (20% bonus), and `rate: 500` the second week).
* set a `cap` to your crowdsale, invalidating any purchases that would exceed that cap (example: sell 70% of tokens and the rest is for team, advisors, …)
* set a minimum and maximum individual’s contributions
* create different rounds (like: PreSale and Crowdsale)
* only allow `whitelist`ed participants to purchase tokens. Useful for putting your KYC / AML whitelist on-chain!
* and more… (visit link below)

**More here:** [**Learn about OpenZeppelin Crowdsales**](https://openzeppelin.org/api/docs/learn-about-crowdsales.html)**.**

You may also want to set up an ICO website with all the information about the ICO dates, rates, cap, etc.\
\\
