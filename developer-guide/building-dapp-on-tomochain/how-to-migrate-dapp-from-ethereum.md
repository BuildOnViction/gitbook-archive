---
description: >-
  Now that we’ve successfully compiled, it’s time to migrate your smart
  contracts to TomoChain’s blockchain!
---

# How to Migrate Dapps from Ethereum

As we previously went through deployment step [here](../smart-contract-development/ides-and-tools/hardhat.md). Change your hardhat configuration to match the following code.

```typescript
import { HardhatUserConfig } from 'hardhat/config';
import '@nomicfoundation/hardhat-toolbox';

require('dotenv').config();

const config: HardhatUserConfig = {
  solidity: {
    version: '0.8.17',
  },
  networks: {
    ...
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
    ...
  },
  defaultNetwork: 'hardhat',
};

export default config;
```

To deploy the contract to the TomoChain, you'll need to modify the scripts/deploy.ts in your project:

{% hint style="info" %}
You should modify your deploy script in order to meet your contract's requirements. This is just an example to deploy Token contract previously presented [here](../smart-contract-development/ides-and-tools/hardhat.md).
{% endhint %}

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

Finally run your script with:

{% hint style="info" %}
Your account (with private key: `process.env.PRIVATE_KEY`) must have enough fund to deploy your contract.
{% endhint %}

* Tomo Testnet

```
npx hardhat run scripts/deploy.ts --network tomo-testnet
```

* Tomo Mainnet

```
npx hardhat run scripts/deploy.ts --network tomo-mainnet
```
