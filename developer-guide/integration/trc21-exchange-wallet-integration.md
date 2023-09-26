---
description: >-
  This tutorial will walk through integrating TRC21 tokens to applications
  (e.g., wallet, exchange)
---

# TRC21 Exchange/Wallet integration

**Prerequisites**

Smart Contract ABI: [TRC21.json](https://raw.githubusercontent.com/tomochain/trc21/master/TRC21.json)

TRC21 Contract Interface:

```
function totalSupply() external view returns (uint256);
function balanceOf(address who) external view returns (uint256);
function estimateFee(uint256 value) external view returns (uint256);
function issuer() external view returns (address);
function allowance(address owner, address spender) external view returns (uint256);
function transfer(address to, uint256 value) external returns (bool);
function approve(address spender, uint256 value) external returns (bool);
function transferFrom(address from, address to, uint256 value) external returns (bool);

event Transfer(address indexed from, address indexed to, uint256 value);
event Approval(address indexed owner, address indexed spender, uint256 value);
event Fee(address indexed from, address indexed to, address indexed issuer, uint256 value);
```

Users are recommended to refer to[ the TRC21 Specification](broken-reference) for more details about the TRC21 token standard.

Follow the steps below to interact with the smart contract by using the Web3 library and Node.

### Initialize Web3 provider <a href="#init-web3-provider" id="init-web3-provider"></a>

As a first step, we need to initialize a Web3 provider by connecting to TomoChain Full node RPC endpoint.

Look at the [TomoChain Networks](../working-with-tomochain/) page to get more information of the TomoChain Testnet/Mainnet RPC network.

```
const Web3 = require('web3')
const web3 = new Web3('https://rpc.tomochain.com')
const chainId = 88
```

### Unlock wallet <a href="#unlock-wallet" id="unlock-wallet"></a>

Unlock the wallet before interacting with TRC21 token contracts

**Example**

```
// Unlock wallet by private key
const account = web3.eth.accounts.privateKeyToAccount(pkey)
const holder = account.address
web3.eth.accounts.wallet.add(account)
web3.eth.defaultAccount = holder
```

### Initialize Web3 TRC21 Contract <a href="#init-web3-trc21-contract" id="init-web3-trc21-contract"></a>

```
const trc21Abi = require('./TRC21.json')
const address = '[enter_your_contract_address]'
const trc21 = new web3.eth.Contract(trc21Abi,
        address, {gasPrice: 250000000, gas: 2000000 })
```

Note: Get TRC21.json [here](https://raw.githubusercontent.com/tomochain/trc21/master/TRC21.json)

### Check balance <a href="#check-balance" id="check-balance"></a>

Call function `balanceOf()` from TRC21 contract to check the token balance for an address.

**Example**

```
trc21.methods.balanceOf(holder).call()
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

### Estimate fee <a href="#estimate-fee" id="estimate-fee"></a>

Before sending tokens, we need to check TX fee by calling `estimateFee` function in TRC21 smart contract.

**Example**

```
trc21.methods.estimateFee().call()
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

Note: this fee is the amount of the token that needs to be paid to send the TRC21 token applied to TomoZ

### Transfer token <a href="#transfer-token" id="transfer-token"></a>

The Token holder needs to call function `transfer` to send token to an address

**Example**

```
// send 500000000000000000000 tokens to this address (e.g decimals 18)
const to = "0xf8ac9d5022853c5847ef75aea0104eed09e5f402"
trc21.methods.transfer(to, '500000000000000000000').send({
    from: holder,
    gas: 2000000,
    gasPrice: 250000000,
    chainId: chainId
})
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

Take a look at this example: [Transfer TRC21 token](https://gist.github.com/thanhson1085/03e983e933dc9cbf7a3d5c88ef503b18)

### Checking TomoZ <a href="#checking-tomoz" id="checking-tomoz"></a>

Call `getTokenCapacity` to https://scan.tomochain.com/address/0x8c0faeb5c6bed2129b8674f262fd45c4e9468bee#readContract. If the return value > 0, the token has successfully been enabled by the TomoZ protocol.
