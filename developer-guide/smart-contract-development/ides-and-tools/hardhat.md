---
description: >-
  This section will guide you through deploying a smart contract on the
  TomoChain using Hardhat.
---

# Hardhat

### Prerequisites[​](https://docs.linea.build/build-on-linea/quickstart/deploy-smart-contract/hardhat#prerequisites) <a href="#user-content-prerequisites" id="user-content-prerequisites"></a>

Before you begin, ensure you've:

* Download [Node v16+](https://nodejs.org/en/download/).
* An ethereum wallet.
* Funded your wallet for caring gas fee of transactions.

### Create a Hardhat project[​](https://docs.base.org/guides/deploy-smart-contracts#node-v18)

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

### Configure hardhat with TomoChain

In order to deploy smart contracts to the TomoChain, you will need to configure your Hardhat project and add the TomoChain network.

To configure Hardhat to use TomoChain, add TomoChain as a network to your project's `hardhat.config.ts` file:

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

### Install Hardhat toolbox

The above configuration uses the `@nomicfoundation/hardhat-toolbox` plugin to bundle all the commonly used packages and Hardhat plugins recommended to start developing with Hardhat.

To install `@nomicfoundation/hardhat-toolbox`, run:

```
npm install --save-dev @nomicfoundation/hardhat-toolbox
```

### Load environment variables

The above configuration also uses [dotenv](https://www.npmjs.com/package/dotenv) to load the `PRIVATE_KEY` environment variable from a `.env` file to `process.env.PRIVATE_KEY`. You should use a similar method to avoid hardcoding your private keys within your source code.

To install `dotenv`, run:

```
npm install --save-dev dotenv
```

Once you have `dotenv` installed, you can create a `.env` file with the following content:

```
PRIVATE_KEY=<YOUR_PRIVATE_KEY>
```

Substitute `<YOUR_PRIVATE_KEY>` with the private key for your wallet.

### Compile the smart contract[​](https://docs.base.org/guides/deploy-smart-contracts#compiling-the-smart-contract) <a href="#compiling-the-smart-contract" id="compiling-the-smart-contract"></a>

Below is a simple token contract (ERC20) written in the Solidity programming language:

```solidity
pragma solidity 0.8.17;

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
npm install --save @openzeppelin/contracts@4.9.3
```

In your project, delete the `contracts/Lock.sol` contract that was generated with the project and add the above code in a new file called `contracts/MyToken.sol.`

To compile the contract using Hardhat, run:

```
npx hardhat compile
```

### Deploy the smart contract[​](https://docs.base.org/guides/deploy-smart-contracts#deploying-the-smart-contract) <a href="#deploying-the-smart-contract" id="deploying-the-smart-contract"></a>

Once your contract has been successfully compiled, you can deploy the contract to the TomoChain networks.

To deploy the contract to the TomoChain testnet, you'll need to modify the `scripts/deploy.ts` in your project:

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

Gas limit is required when deploying a smart contract using Hardhat in TomoChain
{% endhint %}

Finally, ensure your wallet has enough fund to cover gas fee and run script with command:

```
npx hardhat run scripts/deploy.ts --network tomo-testnet
```

The contract will be deployed on the TomoChain testnet. You can view the deployment status and contract by using [TomoScan](https://testnet.tomoscan.io/) and searching for the address returned by your deploy script. If you've deployed an exact copy of the token contract above, it will be verified, and you'll be able to read and write to the contract using the web interface.

### Verify contract on TomoScan

TomoScan now support contract verification via Hardhat API, you will need to change hardhat.config.ts with the following configuration:

```typescript
import { HardhatUserConfig } from "hardhat/config";
import "@nomicfoundation/hardhat-toolbox";

/** @type import('hardhat/config').HardhatUserConfig */
const config: HardhatUserConfig = {
  networks: {
    tomochain: {
      url: "https://rpc.tomochain.com", // for mainnet
      accounts:  ['']
    }
  },

  etherscan: {
    apiKey: {
      goerli: "",
      tomochain: "tomoscan2023",
    },
    customChains: [
      {
        network: "tomochain",
        chainId: 88, // for mainnet
        urls: {
          apiURL: "https://tomoscan.io/api/contract/hardhat/verify", // for mainnet
          browserURL: "https://tomoscan.io", // for mainnet

        }
      }
    ]
  }
};
```
