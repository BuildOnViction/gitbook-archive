---
description: 'TomoChain, the reasonable blockchain choice for Dapp''s.'
---

# Build a Dapp on TomoChain



In this guide we will be covering:

* Setting up Truffle, the most popular development framework for Ethereum which also works perfectly for TomoChain
* Creating a Truffle project
* Creating a TomoChain wallet
* Requesting free tokens using TomoChain faucet
* Writing a smart contract
* Compiling and migrating the smart contract to TomoChain
* Connecting Metamask to TomoChain testnet
* Creating a user interface to interact with the smart contract

### Why should developers build DApps on TomoChain? <a id="8c4b"></a>



Remember [_CryptoKitties_](https://www.cryptokitties.co/) in 2017? A single DApp brought the whole Ethereum blockchain to their knees. The network was congested, with endless waiting times for transaction confirmation and high transaction fees. Porting to TomoChain would seem a good idea for the cute kitties.

TomoChain mainnet can process 2,000 TPS, wich is **100x faster than the Ethereum blockchain,** and for a fraction of the cost. If this is not good enough, the Vietnam-based company is working on its Sharding solution aiming to deliver 20'000–30'000 TPS by Q2 2019.

In this tutorial, we will see **how to build a DApp using Solidity** and then deploy it to **TomoChain** blockchain.

> **Note:** Because deploying a smart contract on mainnet is much similar to testnet, the differences are just the configuration information, this document will explicitly mention the differences where possible

