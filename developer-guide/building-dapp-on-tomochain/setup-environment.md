# Setup Environment

## Prerequisites <a id="7095"></a>

To start building your Dapp you will need to install some programs:

* Install [**Node.js**](https://nodejs.org/en/download/) & **npm** \(“Node.js Package Manager”\)
* Install [**Git**](https://git-scm.com/downloads)

To check that Node is installed properly, open a console \(admin PowerShell on Windows\) and type `node -v`. This should print a version number, like `v10.15.0`.

To test npm, type `npm -v` and you should see the version number, like `6.4.1`.

## Getting Started: Installation <a id="3965"></a>

[**Truffle Framework**](https://truffleframework.com/) is a great tool for developing Dapps. You can use Truffle to deploy your smart contracts to TomoChain.

We only need this single command to install Truffle, the popular development framework for Ethereum.

```text
npm install -g truffle
```

You can verify that Truffle is correctly installed typing `truffle version`.

## Creating a Truffle project <a id="1abb"></a>

Truffle initializes in the current directory, so first create a directory in your development folder of choice and then move inside it.

```text
mkdir pet-shop-tutorialcd pet-shop-tutorial
```

Let’s see [**how to create a Truffle project**](https://truffleframework.com/docs/truffle/getting-started/creating-a-project). ****There are two options. You can create a bare new project from scratch with no smart contracts included, and the other option for those just getting started, you can use [**Truffle Boxes**](https://truffleframework.com/boxes), which are example applications and project templates.

![](https://miro.medium.com/max/60/1*0iPGzZ_MuACqNeSRw1ymUg.png?q=20)![](https://miro.medium.com/max/1024/1*0iPGzZ_MuACqNeSRw1ymUg.png)Pet Shop Truffe Box

There is a special [Truffle Box](https://truffleframework.com/boxes) for this tutorial called **`pet-shop`**, which includes the basic project structure as well as code for the user interface. Use the **`truffle unbox`** command to unpack this Truffle Box:

```text
truffle unbox pet-shop
```

The default Truffle directory structure contains a series of folders and files. If you want to know more, please check [Truffle tutorials](https://truffleframework.com/tutorials/pet-shop#directory-structure).

> **Note:** This tutorial is focused on **the whole process to build a Dapp on TomoChain**, so we will not enter into all the details.

## Creating a TOMO Wallet <a id="a775"></a>

**You will need a wallet address** and some tokens. We will show you how to do it on both TomoChain Testnet and Mainnet.

### 1. Create a TOMO wallet and save your Mnemonic <a id="d296"></a>

You can create a new TOMO wallet using **TomoWallet** mobile app for [iOS](https://itunes.apple.com/us/app/tomo-wallet/id1436476145?mt=8), or the web version \([https://wallet.tomochain.com/\#/login](https://wallet.tomochain.com/#/login)\). Under _Settings_ go to _Advanced Settings,_ here you can _Choose network_ and select `TomoChain TestNet` or `TomoChain` \[mainnet\].

Go to _Settings_ menu, select _Backup wallet_ and then **Continue**. Here you can see your wallet’s private key and the 12-word recovery phrase. **Write down the 12-word recovery phrase.**

You can also create a new [TomoChain wallet with MetaMask, MyEtherWallet or TrustWallet](https://docs.tomochain.com/get-started/wallet/). For instance, for mainnet you can go to [MyEtherWallet](https://www.myetherwallet.com/) and select **TOMO \(tomochain.com\)** on the top right corner. Enter a password and then Create a new wallet. **Write down your recovery phrase.**

For this tutorial, my wallet address \(testnet\) is:

```text
0xc9b694877acd4e2e100e095788a591249c38b9c5
```

My recovery phrase \(12-word `mnemonic`\) is:

```text
myth ahead spin horn minute tag spirit please gospel infant clog camera
```

Write them down. This will be needed later. **Notice that your wallet address \(public key\) and your recovery phrase will be different than mine.**

> **Important!** Always keep your private key and recovery phrase **secret!**

### 2. Get some TOMO funds <a id="3232"></a>

Tokens are required for different matters, like smart contract deployment or to use in Dapps.

**Testnet:** Receive 15 free testnet TOMO tokens using [TomoChain’s Faucet](https://faucet.testnet.tomochain.com/).

**Mainnet:** You need real TOMO tokens from exchanges.

Go to faucet and collect `30 TOMO`. Now your wallet has enough balance to do everything in this tutorial so… let’s go ahead!

### 3. The Block Explorer <a id="07a6"></a>

To check the balance of a wallet address, you can use **TomoScan**.

**Testnet:** [https://scan.testnet.tomochain.com/](https://scan.testnet.tomochain.com/)

**Mainnet:** [https://scan.tomochain.com/](https://scan.tomochain.com/)

