# Ethers.js

### About

The [Ethers.js](https://docs.ethers.org/) library provides a set of tools to interact with Ethereum Nodes with JavaScript, similar to Web3.js. Moonbeam has an Ethereum-like API available that is fully compatible with Ethereum-style JSON-RPC invocations. Therefore, developers can leverage this compatibility and use the Ethers.js library to interact with a Moonbeam node as if they were doing so on Ethereum. For more information on Ethers.js, check their [documentation site](https://docs.ethers.org/v6/).

In this guide, you'll learn how to use the Ethers.js library to send a transaction and deploy a contract on TomoChain.

### Checking Prerequisites  <a href="#user-content-checking-prerequisites" id="user-content-checking-prerequisites"></a>

To test out the examples in this guide on TomoChain [mainnet](https://github.com/c98tristan/gitbook-tomochain/blob/master/developer-guide/working-with-tomochain/tomochain-mainnet.md) or [testnet](https://github.com/c98tristan/gitbook-tomochain/blob/master/developer-guide/working-with-tomochain/tomochain-testnet.md), you will need to have the corresponding RPC API endpoints and some native TOMO tokens.

{% hint style="info" %}
The examples in this guide assumes you have a MacOS or Ubuntu 18.04-based environment and will need to be adapted accordingly for Windows.
{% endhint %}

### Installing Ethers.js  <a href="#user-content-install-ethersjs" id="user-content-install-ethersjs"></a>

To get started, you'll need to start a basic JavaScript project. First, create a directory to store all of the files you'll be creating throughout this guide and initialize the project with the following command:

```bash
mkdir ethers-examples
cd ethers-examples
npm init --y
```

For this guide, you'll need to install the Ethers.js library and the Solidity compiler. To install both NPM packages, you can run the following command:

{% tabs %}
{% tab title="npm" %}
npm install ethers solc@0.8.0
{% endtab %}

{% tab title="yarn" %}
yarn add ethers solc@0.8.0
{% endtab %}
{% endtabs %}

### Setting up the Ethers Provider  <a href="#user-content-setting-up-the-ethers-provider" id="user-content-setting-up-the-ethers-provider"></a>

Throughout this guide, you'll be creating a bunch of scripts that provide different functionality such as sending a transaction, deploying a contract, and interacting with a deployed contract. In most of these scripts you'll need to create an [Ethers provider](https://docs.ethers.org/v6/api/providers/) to interact with the network.

To create a provider, you can take the following steps:

1. Import the `ethers` library.
2. Define the `providerRPC` object, which can include the network configurations for any of the networks you want to send a transaction on. You'll include the `name`, `rpc`, and `chainId` for each network.
3. Create the `provider` using the `ethers.JsonRpcProvider` method.

```javascript
// 1. Import ethers
const ethers = require('ethers');

// 2. Define network configurations
const providerRPC = {
  mainnet: {
    name: 'tomochain-mainnet',
    rpc: 'https://rpc.tomochain.com', // Insert your RPC URL here
    chainId: 88,
  },
};
// 3. Create ethers provider
const provider = new ethers.JsonRpcProvider(providerRPC.mainnet.rpc, {
  chainId: providerRPC.mainnet.chainId,
  name: providerRPC.mainnet.name, 
});
```

Save this code snippet as you'll need it for the scripts that are used in the following sections.

### Send a Transaction  <a href="#user-content-send-a-transaction" id="user-content-send-a-transaction"></a>

During this section, you'll be creating a couple of scripts. The first one will be to check the balances of your accounts before trying to send a transaction. The second script will actually send the transaction.

You can also use the balance script to check the account balances after the transaction has been sent.

#### **Check Balances Script**&#x20;

You'll only need one file to check the balances of both addresses before and after the transaction is sent. To get started, you can create a `balances.js` file by running:

```bash
touch balances.js
```

Next, you will create the script for this file and complete the following steps:

1. [Set up the Ethers provider](https://docs.moonbeam.network/builders/build/eth-api/libraries/ethersjs/#setting-up-the-ethers-provider).
2. Define the `addressFrom` and `addressTo` variables.
3. Create the asynchronous `balances` function which wraps the `provider.getBalance` method.
4. Use the `provider.getBalance` function to fetch the balances for the `addressFrom` and `addressTo` addresses. You can also leverage the `ethers.formatEther` function to transform the balance into a more readable number in TOMO.
5. Lastly, run the `balances` function.

```javascript
// 1. Import ethers
const ethers = require('ethers');

// 2. Define network configurations
const providerRPC = {
  mainnet: {
    name: 'tomochain-mainnet',
    rpc: 'https://rpc.tomochain.com', // Insert your RPC URL here
    chainId: 88,
  },
};
// 3. Create ethers provider
const provider = new ethers.JsonRpcProvider(providerRPC.mainnet.rpc, {
  chainId: providerRPC.mainnet.chainId,
  name: providerRPC.mainnet.name, 
}); // Change to correct network

// Define addresses
const addressFrom = 'INSERT_FROM_ADDRESS';
const addressTo = 'INSERT_TO_ADDRESS';

// Create balances function
const balances = async () => {
  // Fetch balances
  const balanceFrom = ethers.formatEther(
    await provider.getBalance(addressFrom)
  );
  const balanceTo = ethers.formatEther(await provider.getBalance(addressTo));

  console.log(`The balance of ${addressFrom} is: ${balanceFrom} DEV`);
  console.log(`The balance of ${addressTo} is: ${balanceTo} DEV`);
};

// Call the balances function
balances();
```

To run the script and fetch the account balances, you can run the following command:

```
node balances.js
```

If successful, the balances for the origin and receiving address will be displayed in your terminal.

#### **Send Transaction Script**&#x20;

You'll only need one file for executing a transaction between accounts. For this example, you'll be transferring 1 TOMO token from an origin address (from which you hold the private key) to another address. To get started, you can create a `transaction.js` file by running:

```bash
touch transaction.js
```

Next, you will create the script for this file and complete the following steps:

1. [Set up the Ethers provider](https://docs.moonbeam.network/builders/build/eth-api/libraries/ethersjs/#setting-up-the-ethers-provider).
2. Define the `privateKey` and the `addressTo` variables. The private key is required to create a wallet instance. **Note: This is for example purposes only. Never store your private keys in a JavaScript file**.
3. Create a wallet using the `privateKey` and `provider` from the previous steps. The wallet instance is used to sign transactions.
4. Create the asynchronous `send` function which wraps the transaction object and the `wallet.sendTransaction` method.
5. Create the transaction object which only requires the recipient's address and the amount to send. Note that `ethers.parseEther` can be used, which handles the necessary unit conversions from Ether to Wei - similar to using `ethers.parseUnits(value, 'ether')`.
6. Send the transaction using the `wallet.sendTransaction` method and then use `await` to wait until the transaction is processed and the transaction receipt is returned.
7. Lastly, run the `send` function.

```javascript
// 1. Import ethers
const ethers = require('ethers');

// 2. Define network configurations
const providerRPC = {
  mainnet: {
    name: 'tomochain-mainnet',
    rpc: 'https://rpc.tomochain.com', // Insert your RPC URL here
    chainId: 88,
  },
};
// 3. Create ethers provider
const provider = new ethers.JsonRpcProvider(providerRPC.mainnet.rpc, {
  chainId: providerRPC.mainnet.chainId,
  name: providerRPC.mainnet.name, 
}); // Change to correct network

// Define accounts and wallet
const accountFrom = {
  privateKey: 'INSERT_YOUR_PRIVATE_KEY',
};
const addressTo = 'INSERT_TO_ADDRESS';
const wallet = new ethers.Wallet(accountFrom.privateKey, provider);

// Create send function
const send = async () => {
  console.log(
    `Attempting to send transaction from ${wallet.address} to ${addressTo}`
  );

  // Create transaction
  const tx = {
    to: addressTo,
    value: ethers.parseEther('1'),
  };

  // Send transaction and get hash
  const createReceipt = await wallet.sendTransaction(tx);
  await createReceipt.wait();
  console.log(`Transaction successful with hash: ${createReceipt.hash}`);
};

// Call the send function
send();
```

To run the script, you can run the following command in your terminal:

```bash
node transaction.js
```

If the transaction was succesful, in your terminal you'll see the transaction hash has been printed out.

You can also use the `balances.js` script to check that the balances for the origin and receiving accounts have changed.

### **Deploy a Contract**

The contract you'll be compiling and deploying in the next couple of sections is a simple incrementer contract, arbitrarily named `Incrementer.sol`. You can get started by creating a file for the contract:

```bash
touch Incrementer.sol
```

Next, you can add the Solidity code to the file:

```solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

contract Incrementer {
    uint256 public number;

    constructor(uint256 _initialNumber) {
        number = _initialNumber;
    }

    function increment(uint256 _value) public {
        number = number + _value;
    }

    function reset() public {
        number = 0;
    }
}
```

The `constructor` function, which runs when the contract is deployed, sets the initial value of the number variable stored on-chain (the default is `0`). The `increment` function adds the `_value` provided to the current number, but a transaction needs to be sent, which modifies the stored data. Lastly, the `reset` function resets the stored value to zero.

{% hint style="info" %}
This contract is a simple example for illustration purposes only and does not handle values wrapping around.
{% endhint %}

#### **Compile Contract Script**&#x20;

In this section, you'll create a script that uses the Solidity compiler to output the bytecode and interface (ABI) for the `Incrementer.sol` contract. To get started, you can create a `compile.js` file by running:

```bash
touch compile.js
```

Next, you will create the script for this file and complete the following steps:

1. Import the `fs` and `solc` packages.
2. Using the `fs.readFileSync` function, you'll read and save the file contents of `Incrementer.sol` to `source`.
3. Build the `input` object for the Solidity compiler by specifying the `language`, `sources`, and `settings` to be used.
4. Using the `input` object, you can compile the contract using `solc.compile`.
5. Extract the compiled contract file and export it to be used in the deployment script.

```javascript
// 1. Import packages
const fs = require('fs');
const solc = require('solc');

// 2. Get path and load contract
const source = fs.readFileSync('Incrementer.sol', 'utf8');

// 3. Create input object
const input = {
   language: 'Solidity',
   sources: {
      'Incrementer.sol': {
         content: source,
      },
   },
   settings: {
      outputSelection: {
         '*': {
            '*': ['*'],
         },
      },
   },
};
// 4. Compile the contract
const tempFile = JSON.parse(solc.compile(JSON.stringify(input)));
const contractFile = tempFile.contracts['Incrementer.sol']['Incrementer'];

// 5. Export contract data
module.exports = contractFile;
```

#### **Deploy Contract Script**&#x20;

With the script for compiling the `Incrementer.sol` contract in place, you can then use the results to send a signed transaction that deploys it. To do so, you can create a file for the deployment script called `deploy.js`:

```bash
touch deploy.js
```

Next, you will create the script for this file and complete the following steps:

1. Import the contract file from `compile.js`.
2. [Set up the Ethers provider](https://docs.moonbeam.network/builders/build/eth-api/libraries/ethersjs/#setting-up-the-ethers-provider).
3. Define the `privateKey` for the origin account. The private key is required to create a wallet instance. **Note: This is for example purposes only. Never store your private keys in a JavaScript file**.
4. Create a wallet using the `privateKey` and `provider` from the previous steps. The wallet instance is used to sign transactions.
5. Load the contract `bytecode` and `abi` for the compiled contract.
6. Create a contract instance with signer using the `ethers.ContractFactory` function, providing the `abi`, `bytecode`, and `wallet` as parameters.
7. Create the asynchronous `deploy` function that will be used to deploy the contract.
8. Within the `deploy` function, use the `incrementer` contract instance to call `deploy` and pass in the initial value. For this example, you can set the initial value to `5`. This will send the transaction for contract deployment. To wait for a transaction receipt you can use the `deployed` method of the contract deployment transaction.
9. Lastly, run the `deploy` function.

```javascript
// 1. Import ethers
const ethers = require('ethers');

// 2. Define network configurations
const providerRPC = {
  mainnet: {
    name: 'tomochain-mainnet',
    rpc: 'https://rpc.tomochain.com', // Insert your RPC URL here
    chainId: 88,
  },
};
// 3. Create ethers provider
const provider = new ethers.JsonRpcProvider(providerRPC.mainnet.rpc, {
  chainId: providerRPC.mainnet.chainId,
  name: providerRPC.mainnet.name, 
}); // Change to correct network

// Define accounts and wallet
const accountFrom = {
  privateKey: 'INSERT_YOUR_PRIVATE_KEY',
};
let wallet = new ethers.Wallet(accountFrom.privateKey, provider);

// Load contract info
const bytecode = contractFile.evm.bytecode.object;
const abi = contractFile.abi;

// Create contract instance with signer
const incrementer = new ethers.ContractFactory(abi, bytecode, wallet);

// Create deploy function
const deploy = async () => {
  console.log(`Attempting to deploy from account: ${wallet.address}`);

  // Send tx (initial value set to 5) and wait for receipt
  const contract = await incrementer.deploy(5);
  const txReceipt = await contract.deploymentTransaction().wait();

  console.log(`Contract deployed at address: ${txReceipt.contractAddress}`);
};

// Call the deploy function
deploy();
```

To run the script, you can enter the following command into your terminal:

```bash
node deploy.js
```

If successful, the contract's address will be displayed in the terminal.

### **Read Contract Data (Call Methods)**

Call methods are the type of interaction that don't modify the contract's storage (change variables), meaning no transaction needs to be sent. They simply read various storage variables of the deployed contract.

To get started, you can create a file and name it `get.js`:

```bash
touch get.js
```

Then you can take the following steps to create the script:

1. Import the `abi` from the `compile.js` file.
2. [Set up the Ethers provider](https://docs.moonbeam.network/builders/build/eth-api/libraries/ethersjs/#setting-up-the-ethers-provider).
3. Create the `contractAddress` variable using the address of the deployed contract.
4. Create an instance of the contract using the `ethers.Contract` function and passing in the `contractAddress`, `abi`, and `provider`.
5. Create the asynchronous `get` function.
6. Use the contract instance to call one of the contract's methods and pass in any inputs if necessary. For this example, you will call the `number` method which doesn't require any inputs. You can use `await` which will return the value requested once the request promise resolves.
7. Lastly, call the `get` function.

```javascript
// 1. Import ethers
const ethers = require('ethers');
const { abi } = require('./compile');

// 2. Define network configurations
const providerRPC = {
  mainnet: {
    name: 'tomochain-mainnet',
    rpc: 'https://rpc.tomochain.com', // Insert your RPC URL here
    chainId: 88,
  },
};
// 3. Create ethers provider
const provider = new ethers.JsonRpcProvider(providerRPC.mainnet.rpc, {
  chainId: providerRPC.mainnet.chainId,
  name: providerRPC.mainnet.name, 
}); // Change to correct network

// Contract address variable
const contractAddress = 'INSERT_CONTRACT_ADDRESS';

// Create contract instance
const incrementer = new ethers.Contract(contractAddress, abi, provider);

// Create get function
const get = async () => {
  console.log(`Making a call to contract at address: ${contractAddress}`);

  // Call contract
  const data = await incrementer.number();

  console.log(`The current number stored is: ${data}`);
};

// Call get function
get();
```

To run the script, you can enter the following command in your terminal:

```bash
node get.js
```

If successful, the value will be displayed in the terminal.

### **Interact with Contract (Send Methods)**&#x20;

Send methods are the type of interaction that modify the contract's storage (change variables), meaning a transaction needs to be signed and sent. In this section, you'll create two scripts: one to increment and one to reset the incrementer. To get started, you can create a file for each script and name them `increment.js` and `reset.js`:

```bash
touch increment.js reset.js
```

Open the `increment.js` file and take the following steps to create the script:

1. Import the `abi` from the `compile.js` file.
2. [Set up the Ethers provider](https://docs.moonbeam.network/builders/build/eth-api/libraries/ethersjs/#setting-up-the-ethers-provider).
3. Define the `privateKey` for the origin account, the `contractAddress` of the deployed contract, and the `_value` to increment by. The private key is required to create a wallet instance. **Note: This is for example purposes only. Never store your private keys in a JavaScript file**.
4. Create a wallet using the `privateKey` and `provider` from the previous steps. The wallet instance is used to sign transactions.
5. Create an instance of the contract using the `ethers.Contract` function and passing in the `contractAddress`, `abi`, and `provider`.
6. Create the asynchronous `increment` function.
7. Use the contract instance to call one of the contract's methods and pass in any inputs if necessary. For this example, you will call the `increment` method which requires the value to increment by as an input. You can use `await` which will return the value requested once the request promise resolves.
8. Lastly, call the `increment` function.

```javascript
// 1. Import ethers
const ethers = require('ethers');
const { abi } = require('./compile');

// 2. Define network configurations
const providerRPC = {
  mainnet: {
    name: 'tomochain-mainnet',
    rpc: 'https://rpc.tomochain.com', // Insert your RPC URL here
    chainId: 88,
  },
};
// 3. Create ethers provider
const provider = new ethers.JsonRpcProvider(providerRPC.mainnet.rpc, {
  chainId: providerRPC.mainnet.chainId,
  name: providerRPC.mainnet.name, 
}); // Change to correct network

// Create variables
const accountFrom = {
  privateKey: 'INSERT_YOUR_PRIVATE_KEY',
};
const contractAddress = 'INSERT_CONTRACT_ADDRESS';
const _value = 3;

// 4. Create wallet
let wallet = new ethers.Wallet(accountFrom.privateKey, provider);

// 5. Create contract instance with signer
const incrementer = new ethers.Contract(contractAddress, abi, wallet);

// 6. Create increment function
const increment = async () => {
  console.log(
    `Calling the increment by ${_value} function in contract at address: ${contractAddress}`
  );

  // 7. Sign and send tx and wait for receipt
  const createReceipt = await incrementer.increment(_value);
  await createReceipt.wait();

  console.log(`Tx successful with hash: ${createReceipt.hash}`);
};

// 8. Call the increment function
increment();
```

To run the script, you can enter the following command in your terminal:

```bash
node increment.js
```

If successful, the transaction hash will be displayed in the terminal. You can use the `get.js` script alongside the `increment.js` script. Next you can open the `reset.js` file and take the following steps to create the script:

1. Import the `abi` from the `compile.js` file.
2. [Set up the Ethers provider](https://docs.moonbeam.network/builders/build/eth-api/libraries/ethersjs/#setting-up-the-ethers-provider).
3. Define the `privateKey` for the origin account and the `contractAddress` of the deployed contract. The private key is required to create a wallet instance. **Note: This is for example purposes only. Never store your private keys in a JavaScript file**.
4. Create a wallet using the `privateKey` and `provider` from the previous steps. The wallet instance is used to sign transactions.
5. Create an instance of the contract using the `ethers.Contract` function and passing in the `contractAddress`, `abi`, and `provider`.
6. Create the asynchronous `reset` function.
7. Use the contract instance to call one of the contract's methods and pass in any inputs if necessary. For this example, you will call the `reset` method which doesn't require any inputs. You can use `await` which will return the value requested once the request promise resolves.
8. Lastly, call the `reset` function.

```javascript
// 1. Import ethers
const ethers = require('ethers');
const { abi } = require('./compile');

// 2. Define network configurations
const providerRPC = {
  mainnet: {
    name: 'tomochain-mainnet',
    rpc: 'https://rpc.tomochain.com', // Insert your RPC URL here
    chainId: 88,
  },
};
// 3. Create ethers provider
const provider = new ethers.JsonRpcProvider(providerRPC.mainnet.rpc, {
  chainId: providerRPC.mainnet.chainId,
  name: providerRPC.mainnet.name, 
}); // Change to correct network

// Create variables
const accountFrom = {
  privateKey: 'INSERT_YOUR_PRIVATE_KEY',
};
const contractAddress = 'INSERT_CONTRACT_ADDRESS';

// Create wallet
let wallet = new ethers.Wallet(accountFrom.privateKey, provider);

// Create contract instance with signer
const incrementer = new ethers.Contract(contractAddress, abi, wallet);

// Create reset function
const reset = async () => {
  console.log(
    `Calling the reset function in contract at address: ${contractAddress}`
  );

  // Sign and send tx and wait for receipt
  const createReceipt = await incrementer.reset();
  await createReceipt.wait();

  console.log(`Tx successful with hash: ${createReceipt.hash}`);
};

// Call the reset function
reset();
```

To run the script, you can enter the following command in your terminal:

```bash
node reset.js
```

If successful, the transaction hash will be displayed in the terminal. You can use the `get.js` script alongside the `reset.js` script to make sure that value is changing as expected.
