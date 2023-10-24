# Exchange/Wallet integration

TomoChain is an EVM-compatible public blockchain. So you can use [TomoChain JSON-RPC APIs](https://apidocs.tomochain.com/#tomochain-apis-json-rpc) similar as in Ethereum.

EVM compatible libraries such as [Web3.js](../smart-contract-development/ides-and-tools/web3js.md) or [Ethers.js](../smart-contract-development/ides-and-tools/ethers.js.md) library can be fully reused in integration to create a wallet, check wallet balances, or create/send transactions. All you need is to connect to TomoChain's RPC public endpoint. [This tutorial](../working-with-tomochain/) will guide you the steps to connect to TomoChain Testnet/Mainnet using Web3.js.

### Connect to TomoChain's public RPC endpoint <a href="#connect-to-tomochain-nodes" id="connect-to-tomochain-nodes"></a>

```javascript
import Web3 from 'web3';

const web3 = new Web3('https://rpc.tomochain.com');
```

### Create a wallet <a href="#create-wallet" id="create-wallet"></a>

Generate an account object with private key and public key.

```javascript
web3.eth.accounts.create([entropy]);
```

**Example**

```javascript
web3.eth.accounts.create();
> {
    address: "0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01",
    privateKey: "0x348ce564d427a3311b6536bbcff9390d69395b06ed6c486954e971d960fe8709",
    signTransaction: function(tx){...},
    sign: function(data){...},
    encrypt: function(password){...}
}

web3.eth.accounts.create('2435@#@#@±±±±!!!!678543213456764321§34567543213456785432134567');
> {
    address: "0xF2CD2AA0c7926743B1D4310b2BC984a0a453c3d4",
    privateKey: "0xd7325de5c2c1cf0009fac77d3d04a9c004b038883446b065871bc3e831dcd098",
    signTransaction: function(tx){...},
    sign: function(data){...},
    encrypt: function(password){...}
}

web3.eth.accounts.create(web3.utils.randomHex(32));
> {
    address: "0xe78150FaCD36E8EB00291e251424a0515AA1FF05",
    privateKey: "0xcc505ee6067fba3f6fc2050643379e190e087aeffe5d958ab9f2f3ed3800fa4e",
    signTransaction: function(tx){...},
    sign: function(data){...},
    encrypt: function(password){...}
}
```

### Check wallet balances <a href="#wallet-balances" id="wallet-balances"></a>

Get account balance.

```javascript
web3.eth.getBalance(address [, defaultBlock] [, callback])
```

**Example**

```javascript
web3.eth.getBalance("0x407d73d8a49eeb85d32cf465507dd71d507100c1").then(console.log);
> "1000000000000"
```

### Create transaction <a href="#create-transaction" id="create-transaction"></a>

Send transaction to the network. You need to unlock wallet before using this function.

```javascript
web3.eth.sendTransaction(transactionObject [, callback])
```

**Parameters**

1. Object - The transaction object to send:
   * `from` - `String|Number`: The address for the sending account. Uses the web3.eth.defaultAccount property, if not specified. Or an address or index of a local wallet in web3.eth.accounts.wallet.
   * `to` - `String`: (optional) The destination address of the message, left undefined for a contract-creation transaction.
   * `value` - `Number|String|BN|BigNumber`: (optional) The value transferred for the transaction in wei, also the endowment if it’s a contract-creation transaction.
   * `gas` - `Number`: (optional, default: To-Be-Determined) The amount of gas to use for the transaction (unused gas is refunded).
   * `gasPrice` - `Number|String|BN|BigNumber`: (optional) The price of gas for this transaction in wei, defaults to web3.eth.gasPrice.
   * `data` - `String`: (optional) Either a ABI byte string containing the data of the function call on a contract, or in the case of a contract-creation transaction the initialisation code.
   * nonce - `Number`: (optional) Integer of a nonce. This allows to overwrite your own pending transactions that use the same nonce.
2. `callback` - `Function`: (optional) Optional callback, returns an error object as first parameter and the result as second.

**Example**

```javascript
const Web3 = require('web3')

// Connect to TomoChain nodes
const provider = new Web3.providers.HttpProvider('https://rpc.tomochain.com')
const web3 = new Web3(provider)

// Unlock wallet by private key
const account = web3.eth.accounts.privateKeyToAccount(pkey)
let coinbase = account.address
web3.eth.accounts.wallet.add(account)
web3.eth.defaultAccount = coinbase

// Make a transaction using the promise
web3.eth.sendTransaction({
    from: coinbase,
    to: '0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe',
    value: '1000000000000000'
})
.then(function(receipt){
    ...
});
```

### Sign data <a href="#sign-data" id="sign-data"></a>

After unlock a wallet, you can sign some data

```javascript
web3.eth.sign(dataToSign, address [, callback])
```

**Parameters**

1. `String` - Data to sign. If String it will be converted using `web3.utils.utf8ToHex`.
2. `String|Number` - Address to sign data with. Or an address or index of a local wallet in `web3.eth.accounts.wallet`.
3. `Function` - (optional) Optional callback, returns an error object as first parameter and the result as second.

**Example**

```javascript
const Web3 = require('web3')

// Connect to TomoChain nodes
const provider = new Web3.providers.HttpProvider('https://rpc.tomochain.com')
const web3 = new Web3(provider)

// Unlock wallet by private key
const account = web3.eth.accounts.privateKeyToAccount(pkey)
let coinbase = account.address
web3.eth.accounts.wallet.add(account)
web3.eth.defaultAccount = coinbase

// Make a transaction using the promise
web3.eth.sign('testdata').then(function(result){
    console.log(result)
});
```

### Check transaction status <a href="#check-transaction-status" id="check-transaction-status"></a>

```javascript
web3.eth.getTransactionReceipt(hash [, callback])
```

> The receipt is not available for pending transactions and returns null.

**Parameters**

1. String - The transaction hash.
2. Function - (optional) Optional callback, returns an error object as first parameter and the result as second.

**Returns**

Promise returns Object - A transaction receipt object, or null when no receipt was found:

* `status` - `Boolean`: `TRUE` if the transaction was successful, `FALSE`, if the EVM reverted the transaction.
* `blockHash` 32 Bytes - `String`: Hash of the block where this transaction was in.
* `blockNumber` - `Number`: Block number where this transaction was in.
* `transactionHash` 32 Bytes - `String`: Hash of the transaction.
* `transactionIndex` - `Number`: Integer of the transactions index position in the block.
* `from` - `String`: Address of the sender.
* `to` - `String`: Address of the receiver. null when its a contract creation transaction.
* `contractAddress` - `String`: The contract address created, if the transaction was a contract creation, otherwise null.
* `cumulativeGasUsed` - `Number`: The total amount of gas used when this transaction was executed in the block.
* `gasUsed` - `Number`: The amount of gas used by this specific transaction alone.
* `logs` - `Array`: Array of log objects, which this transaction generated.

### Irreversible blocks <a href="#irreversible-blocks" id="irreversible-blocks"></a>

In normal case, you can wait for 60 confirmations, then checking block finality via `eth_getBlockFinalityByNumber` or `eth_getBlockFinalityByHash` API:

* [eth\_getBlockFinalityByNumber](https://apidocs.tomochain.com/#eth\_getblockfinalitybynumber)
* [eth\_getBlockFinalityByHash](https://apidocs.tomochain.com/#eth\_getblockFinalitybyhash)

If `result` >= 75, it means the block with the input hash is finalized, thus irreversible.

### How does TomoChain smart contract work? <a href="#how-does-tomochain-smart-contract-work" id="how-does-tomochain-smart-contract-work"></a>

TomoChain supports Solidity compiler version <= 0.8.17

### Does TomoChain support multi-signature wallets? <a href="#possible-to-create-muti-signature-wallet" id="possible-to-create-muti-signature-wallet"></a>

Yes. Similar to Ethereum, you can use Gnosis MultiSigWallet.

### Run TomoChain node <a href="#run-tomochain-node" id="run-tomochain-node"></a>

Please check [Run TomoChain Fullnode](../../masternode/run-a-full-node/) for details how to run a TomoChain full node.
