# Hardhat

This section will guide you through deploying a smart contract on the Tomo network using [Hardhat](https://hardhat.org/).

Hardhat is a developer tool that provides a simple way to deploy, test, and debug smart contracts.

***

## Prerequisites[​](https://docs.linea.build/build-on-linea/quickstart/deploy-smart-contract/hardhat#prerequisites) <a href="#prerequisites" id="prerequisites"></a>

Before you begin, ensure you've:[​](https://docs.base.org/guides/deploy-smart-contracts#node-v18)

* Download [Node v18+](https://nodejs.org/en/download/).
* An ethereum wallet.
* Funded your wallet for carring gas fee of transactions.

## Create a Hardhat project

To create an empty Hardhat project, run the following commands:

```
mkdir hardhat-tomo-tutorial
cd hardhat-tomo-tutorial
npm init
npm install --save-dev hardhat
npx hardhat
```

Select `Create a TypeScript project` then press _enter_ to confirm the project root.

Select `y` for both adding a `.gitignore` and loading the sample project. It will take a moment for the project setup process to complete.

## Configuring hardhat with Tomo

In order to deploy smart contracts to the Tomo network, you will need to configure your Hardhat project and add the Tomo network.

To configure Hardhat to use Tomo, add Tomo as a network to your project's `hardhat.config.ts` file:

```typescript
import { HardhatUserConfig } from 'hardhat/config';
import '@nomicfoundation/hardhat-toolbox';

require('dotenv').config();

const config: HardhatUserConfig = {
  solidity: {
    version: '0.8.17',
  },
  networks: {
    // for mainnet
    'tomo-mainnet': {
      url: 'https://rpc.tomochain.com',
      accounts: [process.env.PRIVATE_KEY as string],
    },
    // for testnet
    'tomo-testnet': {
      url: 'https://rpc.testnet.tomochain.com',
      accounts: [process.env.PRIVATE_KEY as string],
    },
  },
  defaultNetwork: 'hardhat',
};

export default config;
```

## Install Hardhat toolbox[​](https://docs.base.org/guides/deploy-smart-contracts#install-hardhat-toolbox) <a href="#install-hardhat-toolbox" id="install-hardhat-toolbox"></a>

The above configuration uses the `@nomicfoundation/hardhat-toolbox` plugin to bundle all the commonly used packages and Hardhat plugins recommended to start developing with Hardhat.

To install `@nomicfoundation/hardhat-toolbox`, run:

```
npm install --save-dev @nomicfoundation/hardhat-toolbox
```

## Loading environment variables[​](https://docs.base.org/guides/deploy-smart-contracts#loading-environment-variables) <a href="#loading-environment-variables" id="loading-environment-variables"></a>

The above configuration also uses [dotenv](https://www.npmjs.com/package/dotenv) to load the `PRIVATE_KEY` environment variable from a `.env` file to `process.env.PRIVATE_KEY`. You should use a similar method to avoid hardcoding your private keys within your source code.

To install `dotenv`, run:

```
npm install --save-dev dotenv
```

Once you have `dotenv` installed, you can create a `.env` file with the following content:

```
PRIVATE_KEY=<YOUR_PRIVATE_KEY>
```

Substituting `<YOUR_PRIVATE_KEY>` with the private key for your wallet.

## Compiling the smart contract[​](https://docs.base.org/guides/deploy-smart-contracts#compiling-the-smart-contract) <a href="#compiling-the-smart-contract" id="compiling-the-smart-contract"></a>

Below is a simple token contract (ERC20) written in the Solidity programming language:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor() ERC20("My Token", "MYT") {}

    function mint(address recipient, uint256 amount)
        external
        returns (uint256)
    {
        _mint(recipient, amount);
        return amount;
    }
}
```

The Solidity code above defines a smart contract named `ERC20`. The code uses the `ERC20` interface provided by the [OpenZeppelin Contracts library](https://docs.openzeppelin.com/contracts/4.x/) to create a token smart contract. OpenZeppelin allows developers to leverage battle-tested smart contract implementations that adhere to official ERC standards.

To add the OpenZeppelin Contracts library to your project, run:

```
npm install --save @openzeppelin/contracts
```

\
In your project, delete the `contracts/Lock.sol` contract that was generated with the project and add the above code in a new file called `contracts/MyToken.sol.`

To compile the contract using Hardhat, run:

```
npx hardhat compile
```

## Deploying the smart contract[​](https://docs.base.org/guides/deploy-smart-contracts#deploying-the-smart-contract) <a href="#deploying-the-smart-contract" id="deploying-the-smart-contract"></a>

Once your contract has been successfully compiled, you can deploy the contract to the Tomo networks.

To deploy the contract to the Tomo test network, you'll need to modify the `scripts/deploy.ts` in your project:

```typescript
import { ethers } from 'hardhat';

async function main() {
  const gasLimit = 100_000_000;
  const myToken = await ethers.deployContract('MyToken', { gasLimit });

  await myToken.waitForDeployment();

  console.log('Token Contract Deployed at ' + myToken.target);
}

// We recommend this pattern to be able to use async/await everywhere
// and properly handle errors.
main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

{% hint style="warning" %}
**Note**

Gas limit is required when deploying a smart contract using Hardhat in Tomochain
{% endhint %}

Finally, ensure your wallet has enough fund to cover gas fee and run script with command:

```
npx hardhat run scripts/deploy.ts --network tomo-testnet
```

The contract will be deployed on the Tomo test network. You can view the deployment status and contract by using [Tomoscan](https://testnet.tomoscan.io/) and searching for the address returned by your deploy script. If you've deployed an exact copy of the token contract above, it will already be verified and you'll be able to read and write to the contract using the web interface.
