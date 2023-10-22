---
description: >-
  This tutorial will walk through integrating TRC2 tokens to applications (e.g.,
  wallet, exchange)
---

# TRC25 Exchange/Wallet integration

### **Prerequisites**

Contract ABI: [IVRC25.json](https://raw.githubusercontent.com/tomochain/trc25/main/metadata/IVRC25.json)

Contract Interface: [IVRC25.sol](https://github.com/tomochain/trc25/raw/main/contracts/interfaces/IVRC25.sol)

```solidity
interface IVRC25 {
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);
    event Fee(address indexed from, address indexed to, address indexed issuer, uint256 value);

    function decimals() external view returns (uint8);
    function totalSupply() external view returns (uint256);
    function balanceOf(address owner) external view returns (uint256);
    function issuer() external view returns (address);
    function allowance(address owner, address spender) external view returns (uint256);
    function estimateFee(uint256 value) external view returns (uint256);
    function transfer(address recipient, uint256 value) external returns (bool);
    function approve(address spender, uint256 value) external returns (bool);
    function transferFrom(address from, address to, uint256 value) external  returns (bool);
}
```

Users are recommended to refer to the [TRC25 Specification](../standards-and-specification/trc25-specification.md) for more details about the TRC25 token standard.

Follow the steps below to interact with the smart contract by using the Web3 library and Node.

### Initialize Web3 provider <a href="#init-web3-provider" id="init-web3-provider"></a>

As a first step, we need to initialize a Web3 provider by connecting to TomoChain Full node RPC endpoint.

Look at the [TomoChain Networks](../working-with-tomochain/) page to get more information of the TomoChain Testnet/Mainnet RPC network.

```javascript
const Web3 = require('web3')
const web3 = new Web3('https://rpc.tomochain.com')
const chainId = 88
```

### Unlock wallet <a href="#unlock-wallet" id="unlock-wallet"></a>

Unlock the wallet before interacting with TRC25 token contracts

**Example**

```javascript
// Unlock wallet by private key
const account = web3.eth.accounts.privateKeyToAccount(pkey)
const holder = account.address
web3.eth.accounts.wallet.add(account)
web3.eth.defaultAccount = holder
```

### Initialize Web3 TRC25 Contract <a href="#init-web3-trc21-contract" id="init-web3-trc21-contract"></a>

```javascript
const trc25Abi = require('./IVRC25.json')
const address = '[enter_your_contract_address]'
const trc25 = new web3.eth.Contract(trc25Abi,
        address, {gasPrice: 250000000, gas: 2000000 })
```

Note: Get IVRC21.json [here](https://raw.githubusercontent.com/tomochain/trc25/main/metadata/IVRC25.json).

### Check balance <a href="#check-balance" id="check-balance"></a>

Call function `balanceOf()` from TRC25 contract to check the token balance for an address.

**Example**

```javascript
trc25.methods.balanceOf(holder).call()
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

### Estimate fee <a href="#estimate-fee" id="estimate-fee"></a>

Before sending tokens, we need to check TX fee by calling `estimateFee` function in TRC25 smart contract.

**Example**

```javascript
trc25.methods.estimateFee().call()
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

Note: this fee is the amount of the token that needs to be paid to send the TRC25 token applied to TomoZ

### Transfer token <a href="#transfer-token" id="transfer-token"></a>

The Token holder needs to call function `transfer` to send token to an address.

**Example**

```javascript
// send 500000000000000000000 tokens to this address (e.g decimals 18)
const to = "0xf8ac9d5022853c5847ef75aea0104eed09e5f402"
trc25.methods.transfer(to, '500000000000000000000').send({
    from: holder,
    gas: 2000000,
    gasPrice: 250000000,
    chainId: chainId
})
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

### Checking TomoZ <a href="#checking-tomoz" id="checking-tomoz"></a>

Call `getTokenCapacity` to [0x8c0faeb5c6bed2129b8674f262fd45c4e9468bee](https://tomoscan.io/address/0x8c0faeb5c6bed2129b8674f262fd45c4e9468bee). If the return value > 0, the token has successfully been enabled by the TomoZ protocol.
