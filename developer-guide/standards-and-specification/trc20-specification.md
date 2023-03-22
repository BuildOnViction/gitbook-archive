---
description: >-
  What is a TRC20 standard token & How to integrate a TRC20 token to
  applications (e.g. wallets, exchanges)
---

# TRC20 Specification

TRC20 is an equivalent token standard of ERC20 built on top of the TomoChain blockchain. TRC20 token holders would need to hold a small amount of TOMO to cover the transactions' extremly low fees. **TRC20 tokens can be easily integrated into apps and get listed on centralized exchanges with minimal technical requirements.**&#x20;

Smart Contract ABI: [TRC20.json](https://raw.githubusercontent.com/tomochain/trc20/master/TRC20.json)

### TRC20 Contract Interface

```
function totalSupply() public view returns (uint);
function balanceOf(address tokenOwner) public view returns (uint balance);
function allowance(address tokenOwner, address spender) public view returns (uint remaining);
function transfer(address to, uint tokens) public returns (bool success);
function approve(address spender, uint tokens) public returns (bool success);
function transferFrom(address from, address to, uint tokens) public returns (bool success);

event Transfer(address indexed from, address indexed to, uint tokens);
event Approval(address indexed tokenOwner, address indexed spender, uint tokens);
```

TomoChain provides RPC APIs for developers to use the Web3 library to directly call functions in a  contract.

You can follow the steps below to interact with the smart contract by using Web3 library and NodeJS.

### Init Web3 Provider

In the first step, you will need to init Web3 provider by connecting TomoChain Fullnode RPC endpoint.

You can take a look at the [General page](../../general/how-to-connect-to-tomochain-network/) to get the details of the Testnet/Mainnet network information.

```
const Web3 = require('web3')
const web3 = new Web3('https://rpc.tomochain.com')
const chainId = 88
```

### Unlock Wallet

You need to unlock the wallet before interacting with the TRC20 contract.&#x20;

**Example**

```
// Unlock wallet by private key
const account = web3.eth.accounts.privateKeyToAccount(pkey)
const holder = account.address
web3.eth.accounts.wallet.add(account)
web.eth.defaultAccount = holder
```

### Init Web3 TRC20 Contract

```
const trc20Abi = require('./TRC20.json')
const address = '[enter_your_contract_address]'
const trc20 = new web3.eth.Contract(trc20Abi,
        address, {gasPrice: 250000000, gas: 2000000 })
```

Note: you can get TRC20.json [here](https://raw.githubusercontent.com/tomochain/trc20/master/TRC20.json).&#x20;

### Check Balance

You need to call function `balanceOf()` from TRC20 contract to check your token balance for an address.

**Example**

```
trc20.methods.balanceOf(holder).call()
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

### Estimate TX Fee (gas)

Before sending tokens, you will need to make sure you have enough TOMO to cover the transaction fees.&#x20;

You need to use this method:

```
myContract.methods.myMethod([param1[, param2[, ...]]]).estimateGas(options[, callback])
```

**Example**

```
trc20.methods.transfer(to, '500000000000000000000').estimateGas({
    from: holder
})
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

### Transfer Token

Token holders need to call function `transfer` to send a token to an address.&#x20;

**Example**

```
// send 500000000000000000000 tokens to this address (e.g decimals 18)
const to = "0xf8ac9d5022853c5847ef75aea0104eed09e5f402"
trc20.methods.transfer(to, '500000000000000000000').send({
    from: holder,
    gas: 2000000,
    gasPrice: 250000000,
    chainId: chainId
})
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

You can refer to [Transfer TRC20 script](https://gist.github.com/thanhson1085/3c831416287b0c1f4afbf9fcb3aa05dc).&#x20;
