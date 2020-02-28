---
description: 'How to integrate TRC21 token to applications (e.g., wallets, exchanges)'
---

# TRC21 Specification

Smart Contract ABI: [TRC21.json](https://raw.githubusercontent.com/tomochain/trc21/master/TRC21.json)

### TRC21 Contract Interface

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

Refer to [TRC21 Specification](https://docs.tomochain.com/wp-and-research/specs/trc21_standard/)

TomoChain provides RPC APIs. So you can use Web3 library to directly call the functions in the smart contract.

You can follow the steps below to interact with the smart contract by using Web3 library and NodeJS.

### Init Web3 provider <a id="init-web3-provider"></a>

At the first step, you need init Web3 provider by connecting TomoChain Fullnode RPC endpoint.

You can take a look at the [TomoChain Networks](https://docs.tomochain.com/general/networks/) page to get the details of, and information on the Testnet/Mainnet network.

```text
const Web3 = require('web3')
const web3 = new Web3('https://rpc.tomochain.com')
const chainId = 88
```

### Unlock Wallet <a id="unlock-wallet"></a>

You need to unlock the wallet before interacting with the TRC21 contract.

**Example**

```text
// Unlock wallet by private key
const account = web3.eth.accounts.privateKeyToAccount(pkey)
const holder = account.address
web3.eth.accounts.wallet.add(account)
web3.eth.defaultAccount = holder
```

### Init Web3 TRC21 Contract <a id="init-web3-trc21-contract"></a>

```text
const trc21Abi = require('./TRC21.json')
const address = '[enter_your_contract_address]'
const trc21 = new web3.eth.Contract(trc21Abi,
        address, {gasPrice: 250000000, gas: 2000000 })
```

Note: you can get TRC21.json [here](https://raw.githubusercontent.com/tomochain/trc21/master/TRC21.json)

### Check Balance <a id="check-balance"></a>

You need to call function `balanceOf()` from the TRC21 contract to check your token balance for an address.

**Example**

```text
trc21.methods.balanceOf(holder).call()
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

### Estimate Fee <a id="estimate-fee"></a>

Before sending tokens, we need to check TX fee by calling `estimateFee` function in the TRC21 smart contract.

**Example**

```text
trc21.methods.estimateFee().call()
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

Note: This fee is the amount of token you need to pay to send TRC21 token\(s\) that utilizes TomoZ.

### Transfer Token <a id="transfer-token"></a>

Token holders need to call function `transfer` to send token to an address.

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

