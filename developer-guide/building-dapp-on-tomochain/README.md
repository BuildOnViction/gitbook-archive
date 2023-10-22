# Build a Dapp on TomoChain

In this guide:

* Setting up Hardhat, the most popular development framework for Ethereum which also works perfectly for TomoChain.
* Creating a Hardhat project.
* Creating a TomoChain wallet.
* Requesting free tokens using TomoChain faucet.
* Writing a smart contract.
* Compiling and migrating the smart contract to TomoChain.
* Connecting Metamask to TomoChain Testnet.
* Creating a user interface to interact with the smart contract.

### Why should developers build Dapps on TomoChain? <a href="#8c4b" id="8c4b"></a>

Remember [_CryptoKitties_](https://www.cryptokitties.co/) in 2017? A single Dapp brought the whole Ethereum blockchain to its knees. The network was congested, with endless waiting times for transaction confirmation and high transaction fees. Porting to TomoChain would seem a good idea for the cute kitties.

TomoChain Mainnet can process 2,000 TPS, which is **100x faster than the Ethereum blockchain,** and for a fraction of the cost.

In this tutorial, we will see **how to build a Dapp using Solidity** and then deploy it to **TomoChain** blockchain.

> **Note:** Because deploying a smart contract on Mainnet is much similar to Testnet, the differences are just the configuration information, this document will explicitly mention the differences where possible.
