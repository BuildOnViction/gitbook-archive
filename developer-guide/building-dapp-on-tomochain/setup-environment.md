# Setup Environment

### Prerequisites <a href="#7095" id="7095"></a>

To start building your Dapp you will need to install some programs:

* Install [**Node.js**](https://nodejs.org/en/download/) & **npm** (“Node.js Package Manager”)
* Install [**Git**](https://git-scm.com/downloads)

To check that Node is installed properly, open a console (admin PowerShell on Windows) and type `node -v`. This should print a version number, like `v10.15.0`.

To test npm, type `npm -v` and you should see the version number, like `6.4.1`.

### Install Node.js

{% hint style="info" %}
You can [skip](https://hardhat.org/tutorial/creating-a-new-hardhat-project) this section if you already have a working Node.js `>=16.0` installation. If not, here's how to install it on Ubuntu, MacOS and Windows.
{% endhint %}

#### Linux

For Ubuntu based distro, copy and paste these commands in a terminal:

```bash
sudo apt update
sudo apt install curl git
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Check out this [link](https://nodejs.org/en/download/current) for each platform installers.

#### MacOS

Make sure you have `git` installed.

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
nvm install 16
nvm use 16
nvm alias default 16
npm install npm --global # Upgrade npm to the latest version
```

#### Windows

If you are using Windows, we **strongly recommend** you use Windows Subsystem for Linux (also known as WSL 2). You can use Hardhat without it, but it will work better if you use it.

To install Node.js using WSL 2, please read [this guide](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl).

### Creating a new Hardhat project

We'll install Hardhat using the Node.js package manager (`npm`), which is both a package manager and an online repository for JavaScript code.

You can use other package managers with Node.js, but we suggest you use npm 7 or higher to follow this guide. You should already have it if you followed the previous section's steps.

Open a new terminal and run these commands to create a new folder:

```bash
mkdir hardhat-tutorial
cd hardhat-tutorial
```

```bash
npm init
npm install --save-dev hardhat
npx hardhat init
```

Select `Create an empty hardhat.config.js` with your keyboard and hit enter.

```
$ npx hardhat init
888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888

👷 Welcome to Hardhat v2.18.1 👷‍

? What do you want to do? …
  Create a JavaScript project
  Create a TypeScript project
❯ Create an empty hardhat.config.js
  Quit
```

When Hardhat is run, it searches for the closest `hardhat.config.js` file starting from the current working directory. This file normally lives in the root of your project and an empty `hardhat.config.js` is enough for Hardhat to work. The entirety of your setup is contained in this file.

### Create a TOMO Wallet

**You will need a wallet address** and some tokens. We will show you how to do it on both TomoChain Testnet and Mainnet.

#### 1. Create a TOMO wallet and save your Mnemonic

You can create a new TOMO wallet using **TomoWallet** mobile app for [iOS](https://itunes.apple.com/us/app/tomo-wallet/id1436476145?mt=8), or the web version ([https://wallet.tomochain.com/#/login](https://wallet.tomochain.com/#/login)). Under _Settings_ go to _Advanced Settings,_ here you can _Choose network_ and select `TomoChain TestNet` or `TomoChain` \[mainnet].

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

#### 2. Get some TOMO funds

Tokens are required for different matters, like smart contract deployment or to use in Dapps.

**Testnet:** Receive 15 free testnet TOMO tokens using [TomoChain's Faucet](https://faucet.testnet.tomochain.com/).

**Mainnet:** You need real TOMO tokens from exchanges.

Go to faucet and collect `30 TOMO`. Now your wallet has enough balance to do everything in this tutorial so… let’s go ahead!

#### 3. The Block Explorer

To check the balance of a wallet address, you can use **TomoScan**.

**Mainnet:** [https://tomoscan.io/](https://tomoscan.io/)

**Testnet:** [https://testnet.tomoscan.io/](https://testnet.tomoscan.io/)
