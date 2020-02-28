---
description: >-
  Now that we’ve successfully compiled, it’s time to migrate your smart
  contracts to TomoChain’s blockchain!
---

# How to Migrate Dapp from Ethereum

**A migration is a deployment script meant to alter the state of your application’s contracts**, moving it from one state to the next. _\(More about migrations in the_ [_Truffle documentation_](https://truffleframework.com/docs/truffle/getting-started/running-migrations)_\)._

### Create the migration scripts <a id="4a00"></a>

Open the `migrations/` directory and you will see one JavaScript file: `1_initial_migration_js`. This handles deploying the `Migrations.sol` contract to observe subsequent smart contract migrations, and ensures we don't double-migrate unchanged contracts in the future.

Now we are ready to create our own migration script.

1. Create a new file named `2_deploy_contracts.js` in the `migrations/` directory.
2. Add the following content to the `2_deploy_contracts.js` file:

```text
var Adoption = artifacts.require("Adoption");module.exports = function(deployer) {
  deployer.deploy(Adoption);
};
```

### Configure the migration networks in truffle.js <a id="40aa"></a>

Now we are almost ready to deploy to TomoChain. Let’s see [how to deploy your smart contract to a custom provider](https://truffleframework.com/tutorials/using-infura-custom-provider), any blockchain of your choice, like **TomoChain**.

Before starting the migration, we need to specify the **blockchain** where we want to deploy our smart contracts, specify the **address** to deploy — the wallet we just created, and optionally the gas, gas price, etc.

1. Install Truffle’s `HDWalletProvider`, a separate npm package to find and sign transactions for addresses derived from a 12-word `mnemonic` — in a certain blockchain. \([Read more about HDWalletProvider](https://github.com/trufflesuite/truffle-hdwallet-provider).\)

```text
npm install truffle-hdwallet-provider
```

2. Open `truffle.js` file \(`truffle-config.js` on Windows\). You can edit here the migration settings: networks, chain IDs, gas... The current file has only a single network defined, you can define multiple. We will add three networks to migrate our DApp: `development`, `tomotestnet` and `tomomainnet`.

The [official TomoChain documentation — Networks](https://docs.tomochain.com/general/networks/) is very handy. Both Testnet and Mainnet **network configurations** are described there. We need the `RPC endpoint`, the `Chain id` and the `HD derivation path`.

Replace the `truffle.js` file with this new content:

```text
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
    },    ​tomotestnet: 

     ​provider: () => new HDWalletProvider

       ​mnemonic

       ​"https://testnet.tomochain.com"

       ​0

       ​1

       ​true

       ​"m/44'/889'/0'/0/"

     ​)

     ​network_id: "89"

     ​gas: 2000000

     ​gasPrice: 10000000000000

   ​}    tomomainnet: {
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

3. Remember to **update the `truffle.js` file using your own wallet recovery phrase.** Copy the 12 words obtained previously and paste it as the value of the `mnemonic` variable.

```text
var mnemonic = '<PUT YOUR WALLET 12-WORD RECOVERY PHRASE HERE>';
```

Done. Please, notice the `tomotestnet` network will be used to deploy our smart contract. We have also added the `tomomainnet` network, in case you want to deploy to TomoChain Mainnet. However, if you are familiar with [Ganache](https://truffleframework.com/ganache), you could use the `development` network to do the local test as well if you want to. [_Ganache_](https://truffleframework.com/ganache) _is a locally running personal blockchain for Ethereum development you can use to deploy contracts, develop applications, and run tests._

We have added the migration configuration so **we are now able to deploy to public blockchains like TomoChain** \(both testnet and mainnet\).

> **Warning**: In production, we highly recommend storing the **mnemonic** in another secret file \(loaded from environment variables or a secure secret management system\), to reduce the risk of the mnemonic becoming known. If someone knows your mnemonic, they have all of your addresses and private keys!

_Want to try? With npm package `dotenv` you can load an environment variable from a file `.env`, — then update your truffle.js to use this secret `mnemonic`._

### Start the migration <a id="5eb4"></a>

You should have your smart contract already compiled. Otherwise, now it’s a good time to do it with `truffle compile`.

Back in our terminal, migrate the contract to **TomoChain testnet** network:

```text
truffle migrate --network tomotestnet
```

The migrations will start…

```text
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

```text
0x1c48f603520147f8eebc984fadc944aa300ceab125cf40f77b1bb748460db272
```

The contract address is:

```text
0xB4Bb4FebdA9ec02427767FFC86FfbC6C05Da2A73
```

**Congratulations!** You have already deployed your smart contract to TomoChain. All this in just 8 seconds. We started with `30 TOMO` and the deployment has costed `5.38 TOMO` in gas fees.

> **Note:** The command to deploy to **TomoChain mainnet** is very similar:  
> `truffle migrate --network` **`tomomainnet`**

### \*\*\* Troubleshooting \*\*\* <a id="4dbb"></a>

* **Error: `smart contract creation cost is under allowance`**. **Why?** Increasing transaction fees for smart contract creation is one of the ways TomoChain offers to defend against spamming attacks. **Solution:** edit `truffle.js` and add more gas/gasPrice to deploy.
* **Error: `insufficient funds for gas * price + value`. Why?** You don’t have enough tokens in your wallet for gas fees. **Solution:** you need more funds in your wallet to deploy, go to [faucet](https://faucet.testnet.tomochain.com/) and get more tokens.

### Check the deployment transaction <a id="0b1e"></a>

If you want to verify that your contract was deployed successfully, you can check on **TomoScan** [testnet](https://scan.testnet.tomochain.com/) \(or [mainnet](https://scan.tomochain.com/)\). In the search field, type in the transaction ID for your new contract.

You should see details about the transaction, including the block number where the transaction was secured

.![](https://miro.medium.com/max/60/1*7AlMGUJ6mz316IjIl85xSg.png?q=20)![](https://miro.medium.com/max/2512/1*7AlMGUJ6mz316IjIl85xSg.png)TomoScan transaction

You can also enter your wallet address on the TomoScan search bar. You will find 4 transactions out. Your contract has been successfully deployed to TomoChain.

**Congratulations!** You’ve deployed your contract to TomoChain using Truffle. You have written your first smart contract and deployed it to a public blockchain. It’s time to interact with our smart contract now to make sure it does what we want.

## Testing the smart contract <a id="8f62"></a>

It is a good idea to test your smart contracts. You can write some tests in the `test/` directory and execute with `truffle test`. Find more details on [Truffle’s Pet Shop tutorial](https://truffleframework.com/tutorials/pet-shop#testing-the-smart-contract).

