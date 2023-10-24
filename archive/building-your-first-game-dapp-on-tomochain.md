---
description: >-
  This Guide is on how to develop a simple Smart Contract written in Solidity,
  and deploy it onto the TomoChain Testnet
---

# An Example of Building a Dapp on TomoChain

This article will take you through the process of **building a basic Dapp on TomoChain** — an adoption tracking system for a pet shop!

In this guide we will be covering:

* Setting up Truffle, the most popular development framework for Ethereum which also works perfectly for TomoChain
* Creating a Truffle project
* Creating a TomoChain wallet
* Requesting free tokens using TomoChain faucet
* Writing a smart contract
* Compiling and migrating the smart contract to TomoChain
* Connecting Metamask to TomoChain testnet
* Creating a user interface to interact with the smart contract

## What is TomoChain? <a href="#cd48" id="cd48"></a>

[**TomoChain**](https://tomochain.com/) is a scalable blockchain powered via Proof-of-Stake Voting (PoSV) consensus and used commercially by companies globally. TomoChain achieves 2000 TPS, 2-second blocktime, and \~$0 gas fees without compromising decentralization.

Our mission is to accelerate the onboarding of millions of users by empowering today’s applications with technology that masks the friction of Blockchain, all while retaining its underlying benefits.

The TomoChain blockchain and its product ecosystem allow businesses to build high-performance, feature-rich projects to support speed, privacy, usability, and liquidity.\
.

> Every Dapp running on Ethereum can be easily ported to TomoChain

### Why should developers build Dapps on TomoChain? <a href="#8c4b" id="8c4b"></a>

Remember [_CryptoKitties_](https://www.cryptokitties.co/) in 2017? A single Dapp brought the whole Ethereum blockchain to their knees. The network was congested, with endless waiting times for transaction confirmation and high transaction fees. Porting to TomoChain would seem a good idea for the cute kitties.

TomoChain mainnet can process 2'000 TPS, wich is **100x faster than the Ethereum blockchain,** and for a fraction of the cost.

In this tutorial, we will see **how to build a Dapp using Solidity** and then deploy it to **TomoChain** blockchain.

> **Note:** Because deploying a smart contract on mainnet is much similar to testnet, the differences are just the configuration information, this document will explicitly mention the differences where possible

## 0. Prerequisites <a href="#7095" id="7095"></a>

To start building your Dapp you will need to install some programs:

* Install [**Node.js**](https://nodejs.org/en/download/) & **npm** (“Node.js Package Manager”)
* Install [**Git**](https://git-scm.com/downloads)

To check that Node is installed properly, open a console (admin PowerShell on Windows) and type `node -v`. This should print a version number, like `v10.15.0`.

To test npm, type `npm -v` and you should see the version number, like `6.4.1`.

## 1. Getting Started: Installation <a href="#3965" id="3965"></a>

[**Truffle Framework**](https://truffleframework.com/) is a great tool for developing Dapps. You can use Truffle to deploy your smart contracts to TomoChain.

We only need this single command to install Truffle, the popular development framework for Ethereum.

```
npm install -g truffle
```

You can verify that Truffle is correctly installed typing `truffle version`.

## 2. Creating a Truffle project <a href="#1abb" id="1abb"></a>

Truffle initializes in the current directory, so first create a directory in your development folder of choice and then move inside it.

```
mkdir pet-shop-tutorialcd pet-shop-tutorial
```

Let’s see [**how to create a Truffle project**](https://truffleframework.com/docs/truffle/getting-started/creating-a-project). There are two options. You can create a bare new project from scratch with no smart contracts included, and the other option for those just getting started, you can use [**Truffle Boxes**](https://truffleframework.com/boxes), which are example applications and project templates.

![](<../.gitbook/assets/image (74).png>)

There is a special [Truffle Box](https://truffleframework.com/boxes) for this tutorial called **`pet-shop`**, which includes the basic project structure as well as code for the user interface. Use the **`truffle unbox`** command to unpack this Truffle Box:

```
truffle unbox pet-shop
```

The default Truffle directory structure contains a series of folders and files. If you want to know more, please check [Truffle tutorials](https://truffleframework.com/tutorials/pet-shop#directory-structure).

> **Note:** **This tutorial is focused on the whole process to build a Dapp on TomoChain, so we will not enter into all the details.**

## 3. Creating a TOMO Wallet <a href="#a775" id="a775"></a>

**You will need a wallet address** and some tokens. We will show you how to do it on both TomoChain Testnet and Mainnet.

### 3.1 Create a TOMO wallet and save your Mnemonic <a href="#d296" id="d296"></a>

You can create a new TOMO wallet using **TomoWallet** mobile app for [iOS](https://itunes.apple.com/us/app/tomo-wallet/id1436476145?mt=8) or [the web version](https://wallet.tomochain.com/#/login). Under _Settings_ go to _Advanced Settings,_ here you can _Choose network_ and select `TomoChain TestNet` or `TomoChain` \[mainnet].

Go to _Settings_ menu, select _Backup wallet_ and then **Continue**. Here you can see your wallet’s private key and the 12-word recovery phrase. **Write down the 12-word recovery phrase.**

You can also create a new [TomoChain wallet with MetaMask, MyEtherWallet or TrustWallet](https://docs.tomochain.com/get-started/wallet/). For instance, for mainnet you can go to [MyEtherWallet](https://www.myetherwallet.com/) and select **TOMO (tomochain.com)** on the top right corner. Enter a password and then Create a new wallet. **Write down your recovery phrase.**

For this tutorial, my wallet address (testnet) is:

```
0xc9b694877acd4e2e100e095788a591249c38b9c5
```

My recovery phrase (12-word `mnemonic`) is:

```
myth ahead spin horn minute tag spirit please gospel infant clog camera
```

Write them down. This will be needed later. **Notice that your wallet address (public key) and your recovery phrase will be different than mine.**

> **Important!** Always keep your private key and recovery phrase **secret!**

### 3.2 Get some TOMO funds <a href="#3232" id="3232"></a>

Tokens are required for different matters, like smart contract deployment or to use in DApps.

**Testnet:** Receive 15 free testnet TOMO tokens using [TomoChain’s Faucet](https://faucet.testnet.tomochain.com/).

**Mainnet:** You need real TOMO tokens from exchanges.

Go to faucet and collect `30 TOMO`. Now your wallet has enough balance to do everything in this tutorial so… let’s go ahead!

### 3.3 The Block Explorer <a href="#07a6" id="07a6"></a>

To check the balance of a wallet address, you can use **TomoScan**.

**Testnet:** [https://testnet.tomoscan.io/](https://testnet.tomoscan.io/)

**Mainnet:** [https://tomoscan.io/](https://tomoscan.io/)

## 4. Writing the smart contract <a href="#d658" id="d658"></a>

We’ll start our Dapp by writing the smart contract that acts as the back-end logic and storage.

1. Create a new file named `Adoption.sol` in the `contracts/` directory.
2. Copy the following code:

```
pragma solidity ^0.5.0;contract Adoption {
  address[16] public adopters;  // Adopting a pet
  function adopt(uint petId) public returns (uint) {
    // check that petId is in range of our adopters array
    require(petId >= 0 && petId <= 15);    // add the address who called this function to our adopter array
    adopters[petId] = msg.sender;    // return the petId provided as a confirmation
    return petId;
  }  // Retrieving the adopters
  function getAdopters() public view returns (address[16] memory) {
    return adopters;
  }
}
```

> **Note:** Code from [Truffle’s Pet-Shop tutorial](https://truffleframework.com/tutorials/pet-shop#writing-the-smart-contract) — if you want to look deeper into the Solidity code, they slowly go through the Truffle link explaining the details.

## 5. Compiling <a href="#df38" id="df38"></a>

Solidity is a compiled language, meaning we need to compile our Solidity to bytecode for the **Ethereum Virtual Machine (EVM)** to execute. Think of it as translating our human-readable Solidity into something the EVM understands.

> TomoChain is EVM-compatible, which means that every contract written in Ethereum can be seamlessly ported to TomoChain without effort

In a terminal, make sure you are in the root of the directory that contains the Dapp and type:

```
truffle compile
```

You should see output similar to the following:

```
Compiling ./contracts/Migrations.sol... 
Compiling ./contracts/Adoption.sol... 
Writing artifacts to ./build/contracts
```

## 6. Migration — Deploying <a href="#6b08" id="6b08"></a>

Now that we’ve successfully compiled, it’s time to **migrate your smart contracts to TomoChain blockchain!**

**A migration is a deployment script meant to alter the state of your application’s contracts**, moving it from one state to the next. _(More about migrations in the_ [_Truffle documentation_](https://truffleframework.com/docs/truffle/getting-started/running-migrations)_)._

### 6.1 Create the migration scripts <a href="#4a00" id="4a00"></a>

Open the `migrations/` directory and you will see one JavaScript file: `1_initial_migration_js`. This handles deploying the `Migrations.sol`contract to observe subsequent smart contract migrations, and ensures we don't double-migrate unchanged contracts in the future.

Now we are ready to create our own migration script.

1. Create a new file named `2_deploy_contracts.js` in the `migrations/`directory.
2. Add the following content to the `2_deploy_contracts.js` file:

```
var Adoption = artifacts.require("Adoption");module.exports = function(deployer) {
  deployer.deploy(Adoption);
};
```

### 6.2 Configure the migration networks in truffle.js <a href="#40aa" id="40aa"></a>

Now we are almost ready to deploy to TomoChain. Let’s see [how to deploy your smart contract to a custom provider](https://truffleframework.com/tutorials/using-infura-custom-provider), any blockchain of your choice, like **TomoChain**.

Before starting the migration, we need to specify the **blockchain** where we want to deploy our smart contracts, specify the **address** to deploy — the wallet we just created, and optionally the gas, gas price, etc.

1\. Install Truffle’s `HDWalletProvider`, a separate npm package to find and sign transactions for addresses derived from a 12-word `mnemonic` — in a certain blockchain. ([Read more about HDWalletProvider](https://github.com/trufflesuite/truffle-hdwallet-provider).)

```
npm install truffle-hdwallet-provider
```

2\. Open `truffle.js` file (`truffle-config.js` on Windows). You can edit here the migration settings: networks, chain IDs, gas... The current file has only a single network defined, you can define multiple. We will add three networks to migrate our Dapp: `development`, `tomotestnet` and `tomomainnet`.

[The official TomoChain documentation — Networks](../developer-guide/working-with-tomochain/) is very handy. Both Testnet and Mainnet **network configurations** are described there. We need the `RPC endpoint`, the `Chain id` and the `HD derivation path`.

Replace the `truffle.js` file with this new content:

```
'use strict'var HDWalletProvider = require("truffle-hdwallet-provider");var mnemonic = '<PUT YOUR WALLET 12-WORD RECOVERY PHRASE HERE>';module.exports = {
  networks: {
    development: {
      provider: () => new HDWalletProvider(
        mnemonic,
        "http://127.0.0.1:8545",
      ),
      host: "127.0.0.1",
      port: "8545",
      network_id: "*", // Match any network id
    },    tomotestnet: {
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
      gasPrice: 10000000000000,
    },    tomomainnet: {
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
      gasPrice: 10000000000000,
    }
  }
};
```

3\. Remember to **update the `truffle.js` file using your own wallet recovery phrase.** Copy the 12 words obtained previously and paste it as the value of the `mnemonic` variable.

```
var mnemonic = '<PUT YOUR WALLET 12-WORD RECOVERY PHRASE HERE>';
```

Done. Please notice the `tomotestnet` network will be used to deploy our smart contract. We have also added the `tomomainnet` network, in case you want to deploy to TomoChain Mainnet. However, if you are familiar with [Ganache](https://truffleframework.com/ganache), you could use the `development` network to do the local test as well if you want to. [_Ganache_](https://truffleframework.com/ganache) _is a locally running personal blockchain for Ethereum development you can use to deploy contracts, develop applications, and run tests._

We have added the migration configuration so **we are now able to deploy to public blockchains like TomoChain** (both testnet and mainnet).

> **Warning**: In production, we highly recommend storing the **mnemonic** in another secret file (loaded from environment variables or a secure secret management system), to reduce the risk of the mnemonic becoming known. If someone knows your mnemonic, they have all of your addresses and private keys!

_Want to try? With npm package `dotenv` you can load an environment variable from a file `.env`, — then update your truffle.js to use this secret `mnemonic`._

### 6.3 Start the migration <a href="#5eb4" id="5eb4"></a>

You should have your smart contract already compiled. Otherwise, now it’s a good time to do it with `truffle compile`.

Back in our terminal, migrate the contract to **TomoChain testnet** network:

```
truffle migrate --network tomotestnet
```

The migrations will start…

```
Starting migrations...
======================
> Network name:    'tomotestnet'
> Network id:      89
> Block gas limit: 840000001_initial_migration.js
======================Deploying 'Migrations'
   ----------------------
   > transaction hash:    0x77d9cdf0fb810fd6cec8a5616a3519e7fa5d42ad07506802f0b6bc10fa9e8619
   > Blocks: 2            Seconds: 4
   > contract address:    0xA3919059C38b1783Ac41C336AAc6438ac5fd639d
   > account:             0xc9b694877AcD4e2E100e095788A591249c38b9c5
   > balance:             27.15156
   > gas used:            284844
   > gas price:           10000 gwei
   > value sent:          0 ETH
   > total cost:          2.84844 ETH> Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:             2.84844 ETH2_deploy_contracts.js
=====================Deploying 'Adoption'
   --------------------
   > transaction hash:    0x1c48f603520147f8eebc984fadc944aa300ceab125cf40f77b1bb748460db272
   > Blocks: 2            Seconds: 4
   > contract address:    0xB4Bb4FebdA9ec02427767FFC86FfbC6C05Da2A73
   > account:             0xc9b694877AcD4e2E100e095788A591249c38b9c5
   > balance:             24.19238
   > gas used:            253884
   > gas price:           10000 gwei
   > value sent:          0 ETH
   > total cost:          2.53884 ETH> Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:             2.53884 ETHSummary
=======
> Total deployments:   2
> Final cost:          5.38728 ETH
```

The transaction ID is:

```
0x1c48f603520147f8eebc984fadc944aa300ceab125cf40f77b1bb748460db272
```

The contract address is:

```
0xB4Bb4FebdA9ec02427767FFC86FfbC6C05Da2A73
```

**Congratulations!** You have already deployed your smart contract to TomoChain. All this in just 8 seconds. We started with `30 TOMO` and the deployment has costed `5.38 TOMO` in gas fees.

> **Note:** The command to deploy to **TomoChain mainnet** is very similar:\
> ` truffle migrate --network`` `` `**`tomomainnet`**

### \*\*\* Troubleshooting \*\*\* <a href="#4dbb" id="4dbb"></a>

* **Error: `smart contract creation cost is under allowance`**. **Why?** Increasing transaction fees for smart contract creation is one of the ways TomoChain defends against spamming attacks. **Solution:** edit `truffle.js` and add more gas/gas Price to deploy.
* **Error: `insufficient funds for gas * price + value`. Why?** You don’t have enough tokens in your wallet for gas fees. **Solution:** you need more funds in your wallet to deploy, go to [faucet](https://faucet.testnet.tomochain.com/) and get more tokens.

### 6.4 Check the deployment transaction <a href="#0b1e" id="0b1e"></a>

If you want to verify that your contract was deployed successfully, you can check on **TomoScan** [testnet](https://testnet.tomoscan.io/) (or [mainnet](https://tomoscan.io/)). In the search field, type in the transaction ID for your new contract.

You should see details about the transaction, including the block number where the transaction was secured.

![](<../.gitbook/assets/image (32).png>)

You can also enter your wallet address on the TomoScan search bar. You will find 4 transactions out. Your contract has been successfully deployed to TomoChain.

**Congratulations!** You’ve deployed your contract to TomoChain using Truffle. You have written your first smart contract and deployed it to a public blockchain. It’s time to interact with our smart contract now to make sure it does what we want.

## 7. Testing the smart contract <a href="#8f62" id="8f62"></a>

It is a good idea to test your smart contracts. You can write some tests in the `test/` directory and execute with `truffle test`. Find more details on [Truffle’s Pet Shop tutorial](https://truffleframework.com/tutorials/pet-shop#testing-the-smart-contract).

## 8. Creating a user interface to interact with the smart contract <a href="#5a54" id="5a54"></a>

Now **we’ve created the smart contract and deployed it to TomoChain blockchain (testnet).** It’s time to create a UI so that people can use the shop!

Included with the `pet-shop` Truffle Box was code for the app’s front-end. That code exists within the `src/` directory.

The front-end doesn’t use a build system (webpack, grunt, etc.) to be as easy as possible to get started. The structure of the app is already there; we’ll add in the functions unique to Ethereum.

1\. Open `/src/js/app.js` in a text editor.

2\. Examine the file. Note that there is a global `App` object to manage our application, load in the pet data in `init()` and then call the function `initWeb3()`. The [web3 JavaScript library](https://github.com/ethereum/web3.js/) interacts with the Ethereum blockchain. It can retrieve user accounts, send transactions, interact with smart contracts, and more.

3\. The current file has some _incomplete functions_ that you must fill in. Replace the old code and paste this **new code**:

```
App = {
  web3Provider: null,
  contracts: {},
  init: async function() {
    // Load pets.
    $.getJSON('../pets.json', function(data) {
      var petsRow = $('#petsRow');
      var petTemplate = $('#petTemplate');
      for (i = 0; i < data.length; i ++) {
        petTemplate.find('.panel-title').text(data[i].name);
        petTemplate.find('img').attr('src', data[i].picture);
        petTemplate.find('.pet-breed').text(data[i].breed);
        petTemplate.find('.pet-age').text(data[i].age);
        petTemplate.find('.pet-location').text(data[i].location);
        petTemplate.find('.btn-adopt').attr('data-id', data[i].id);
        petsRow.append(petTemplate.html());
      }
    });
    return await App.initWeb3();
  },  initWeb3: async function() {
    //----
    // Modern dapp browsers...
    if (window.ethereum) {
      App.web3Provider = window.ethereum;
      try {
        // Request account access
        await window.ethereum.enable();
      } catch (error) {
        // User denied account access...
        console.error("User denied account access")
      }
    }
    // Legacy dapp browsers...
    else if (window.web3) {
      App.web3Provider = window.web3.currentProvider;
    }
    // If no injected web3 instance is detected, fall back to Ganache
    else {
      App.web3Provider = new     Web3.providers.HttpProvider('http://localhost:7545');
    }
    web3 = new Web3(App.web3Provider);
    //----
    return App.initContract();
  },  initContract: function() {
    //----
    $.getJSON('Adoption.json', function(data) {
      // Get the necessary contract artifact file and instantiate it with truffle-contract
      var AdoptionArtifact = data;
      App.contracts.Adoption = TruffleContract(AdoptionArtifact);      // Set the provider for our contract
      App.contracts.Adoption.setProvider(App.web3Provider);      // Use our contract to retrieve and mark the adopted pets
      return App.markAdopted();
    });
    //----    return App.bindEvents();
  },  bindEvents: function() {
    $(document).on('click', '.btn-adopt', App.handleAdopt);
  },  markAdopted: function(adopters, account) {
    //----
    var adoptionInstance;
    App.contracts.Adoption.deployed().then(function(instance) {
      adoptionInstance = instance;      return adoptionInstance.getAdopters.call();
    }).then(function(adopters) {
      for (i = 0; i < adopters.length; i++) {
        if (adopters[i] !== '0x0000000000000000000000000000000000000000') {
          $('.panel-pet').eq(i).find('button').text('Success').attr('disabled', true);
        }
      }
    }).catch(function(err) {
      console.log(err.message);
    });
    //----
  },  handleAdopt: function(event) {
    event.preventDefault();    var petId = parseInt($(event.target).data('id'));    //----
    var adoptionInstance;    web3.eth.getAccounts(function(error, accounts) {
      if (error) {
        console.log(error);
      }      var account = accounts[0];      App.contracts.Adoption.deployed().then(function(instance) {
        adoptionInstance = instance;        // Execute adopt as a transaction by sending account
        return adoptionInstance.adopt(petId, {from: account});
      }).then(function(result) {
        return App.markAdopted();
      }).catch(function(err) {
        console.log(err.message);
      });
    });
    //---
  }
};$(function() {
  $(window).load(function() {
    App.init();
  });
});
```

Here is what these functions do:

`initWeb3()` Checks if we are using modern DApp browsers or the more recent versions of [MetaMask](https://github.com/MetaMask).

`initContract()` Retrieves the artifact file for our smart contract. **Artifacts are information about our contract such as its deployed address and Application Binary Interface (ABI)**. **The ABI is a JavaScript object defining how to interact with the contract including its variables, functions and their parameters.** We then call the app's `markAdopted()`function in case any pets are already adopted from a previous visit.

`markAdopted()` After calling `getAdopters()`, we then loop through all of them, checking to see if an address is stored for each pet. Ethereum initializes the array with 16 empty addresses. This is why we check for an empty address string rather than null or other false value. Once a `petId`with a corresponding address is found, we disable its Adopt button and change the button text to "Success", so the user gets some feedback.

`handleAdopt()` We get the deployed contract and store the instance in `adoptionInstance`. We're going to send a **transaction** instead of a call by executing the `adopt()` function with both the pet's ID and an object containing the account address. Then, we proceed to call our `markAdopted()`function to sync the UI with our newly stored data.

## 9. Interacting with the Dapp in a browser <a href="#5700" id="5700"></a>

Now we’re ready to use our Dapp!

### 9.1 Install and configure MetaMask <a href="#4986" id="4986"></a>

1. Install the [MetaMask browser extension](https://metamask.io/) in Chrome or FireFox.
2. Once installed, you’ll see the MetaMask fox icon next to your address bar. Click the icon and MetaMask will open up.
3. Create a New password. Then, write down the Secret Backup Phrase and accept the terms. By default, MetaMask will create a new Ethereum address for you.

![](<../.gitbook/assets/image (72).png>)

4\. Now we’re connected to the Ethereum network,with a brand new wallet with 0 ETH.

5\. Let’s now connect MetaMask to TomoChain (testnet). Click the menu with the “Main Ethereum Network” and select **Custom RPC**. Use the[ Networks data from TomoChain](../developer-guide/working-with-tomochain/tomochain-testnet.md) (testnet) and click **Save**.

![](<../.gitbook/assets/image (52).png>)

6\. The network name at the top will switch to say “TomoChain testnet”. Now that we are on TomoChain network we can import TomoChain wallets.

We could use the TOMO wallet we created previously, but better **let’s create a new TOMO wallet** and add a few TOMO tokens — _you know how to do it_.

7\. Once you have created your new TOMO wallet, **copy the private key**. Back to MetaMask, click on the top-right circle and select **Import Account.** Paste the private key and _voilà_! Your TOMO wallet is loaded in MetaMask.

![](<../.gitbook/assets/image (36).png>)

### 9.2 Using the Dapp <a href="#9432" id="9432"></a>

We will now start a local web server and interact with the Dapp. We’re using the `lite-server`. This shipped with the `pet-shop` Truffle box.

The settings for this are in the files `bs-config.json` and `package.json`, if you want to take a look. These tell npm to run our local install of `lite-server`when we execute `npm run dev` from the console.

1. Start the local web server:

```
npm run dev
```

The dev server will launch and automatically open a new browser tab containing your DApp.

![](<../.gitbook/assets/image (71).png>)

Normally, a MetaMask notification automatically requests a connection.

2\. To use the Dapp, click the **Adopt** button on the pet of your choice.

3\. You’ll be automatically prompted to aprove the transaction by MetaMask. Set some Gas and click **Confirm** to approve the transaction.\
\\

![](<../.gitbook/assets/image (55).png>)

4\. You’ll see the button next to the adopted pet change to say **“Success”** and become disabled, just as we specified, because the pet has now been adopted.

![](<../.gitbook/assets/image (42).png>)

And in MetaMask you’ll see the transaction listed:

![](<../.gitbook/assets/image (10).png>)

**Congratulations!** You have taken a huge step to becoming a full-fledged Dapp developer. You have all the tools you need to start making more advanced Dapps and now you can make your Dapp live for others to use deploying to TomoChain.

### &#x20;<a href="#8c4b" id="8c4b"></a>
