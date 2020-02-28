---
description: >-
  This tutorial will walk you through integrating TRC21 tokens to applications
  (e.g., wallet, exchange)
---

# TRC21 Exchange/Wallet integration

**Prerequisites**

Smart Contract ABI: [TRC21.json](https://raw.githubusercontent.com/tomochain/trc21/master/TRC21.json)

TRC21 Contract Interface:

```text
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

Users are recommended to refer to the [TRC21 Specification](https://docs.tomochain.com/wp-and-research/specs/trc21_standard/) for more details about TRC21 token standard.

You can follow the following steps below to interact with the smart contract by using Web3 library and Node.

### Initialize Web3 provider <a id="init-web3-provider"></a>

As a first step, we need to initialize a Web3 provider by connecting to TomoChain Full node RPC endpoint.

You can take a look to [TomoChain Networks](https://docs.tomochain.com/general/networks/) page to get the details of TomoChain Testnet/Mainnet RPC network information.

```text
const Web3 = require('web3')
const web3 = new Web3('https://rpc.tomochain.com')
const chainId = 88
```

### Unlock wallet <a id="unlock-wallet"></a>

You need to unlock the wallet before interacting with TRC21 token contracts

**Example**

```text
// Unlock wallet by private key
const account = web3.eth.accounts.privateKeyToAccount(pkey)
const holder = account.address
web3.eth.accounts.wallet.add(account)
web3.eth.defaultAccount = holder
```

### Initialize Web3 TRC21 Contract <a id="init-web3-trc21-contract"></a>

```text
const trc21Abi = require('./TRC21.json')
const address = '[enter_your_contract_address]'
const trc21 = new web3.eth.Contract(trc21Abi,
        address, {gasPrice: 250000000, gas: 2000000 })
```

Note: you can get TRC21.json [here](https://raw.githubusercontent.com/tomochain/trc21/master/TRC21.json)

### Check balance <a id="check-balance"></a>

You need to call function `balanceOf()` from TRC21 contract to check your token balance for an address.

**Example**

```text
trc21.methods.balanceOf(holder).call()
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

### Estimate fee <a id="estimate-fee"></a>

Before sending tokens, we need to check TX fee by calling `estimateFee` function in TRC21 smart contract.

**Example**

```text
trc21.methods.estimateFee().call()
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

Note: this fee is amount token you need to pay to send TRC21 token that applied TomoZ

### Transfer token <a id="transfer-token"></a>

Token holder needs to call function `transfer` to send token to an address

**Example**

```text
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

You can take a look to this example [Transfer TRC21 token](https://gist.github.com/thanhson1085/03e983e933dc9cbf7a3d5c88ef503b18)

### Checking TomoZ <a id="checking-tomoz"></a>

You need to call `getTokenCapacity` to https://scan.tomochain.com/address/0x8c0faeb5c6bed2129b8674f262fd45c4e9468bee\#readContract. If the return value &gt; 0, the token has successfully been enabled TomoZ protocol.

