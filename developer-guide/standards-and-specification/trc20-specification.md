---
description: >-
  What is a TRC20 standard token & How to integrate a TRC20 token to
  applications (e.g. wallets, exchanges)
---

# TRC20 Specification

TRC20 is an equivalent token standard of ERC20 built on top of the TomoChain blockchain. TRC20 token holders would need to hold a small amount of TOMO to cover the transactions' extremly low fees. **TRC20 tokens can be easily integrated into apps and get listed on centralized exchanges with minimal technical requirements.** 

Smart Contract ABI: [TRC20.json](https://raw.githubusercontent.com/tomochain/trc20/master/TRC20.json)

### TRC20 Contract Interface

```text
function totalSupply() public view returns (uint);
function balanceOf(address tokenOwner) public view returns (uint balance);
function allowance(address tokenOwner, address spender) public view returns (uint remaining);
function transfer(address to, uint tokens) public returns (bool success);
function approve(address spender, uint tokens) public returns (bool success);
function transferFrom(address from, address to, uint tokens) public returns (bool success);

event Transfer(address indexed from, address indexed to, uint tokens);
event Approval(address indexed tokenOwner, address indexed spender, uint tokens);
```

TomoChain provides RPC APIs. So you can use Web3 library to directly call the functions in the smart contract.

You can follow the steps below to interact with the smart contract by using Web3 library and NodeJS.

### Init Web3 Provider

 the first step, you will need init Web3 provider by connecting TomoChain Fullnode RPC endpoint.

You can take a look at the [TomoChain Networks](https://docs.tomochain.com/general/networks/) page to get the details of  Testnet/Mainnet network information.

```text
const Web3 = require('web3')
const web3 = new Web3('https://rpc.tomochain.com')
const chainId = 88
```

### Unlock Wallet

To create a wallet, you can refer to [Create wallet page](https://docs.tomochain.com/developers/integrations/#create-wallet).

You need to unlock the wallet before interacting with the TRC20 contract. 

**Example**

```text
// Unlock wallet by private key
const account = web3.eth.accounts.privateKeyToAccount(pkey)
const holder = account.address
web3.eth.accounts.wallet.add(account)
web.eth.defaultAccount = holder
```

### Init Web3 TRC20 Contract

```text
const trc20Abi = require('./TRC20.json')
const address = '[enter_your_contract_address]'
const trc20 = new web3.eth.Contract(trc20Abi,
        address, {gasPrice: 250000000, gas: 2000000 })
```

Note: you can get TRC20.json [here](https://raw.githubusercontent.com/tomochain/trc20/master/TRC20.json). 

### Check Balance

You need to call function `balanceOf()` from TRC20 contract to check your token balance for an address.

**Example**

```text
trc20.methods.balanceOf(holder).call()
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

### Estimate TX Fee \(gas\)

Before sending tokens, you will need to make sure you have enough TOMO to cover the transaction .

You need to use this method:

```text
myContract.methods.myMethod([param1[, param2[, ...]]]).estimateGas(options[, callback])
```

**Example**

```text
trc20.methods.transfer(to, '500000000000000000000').estimateGas({
    from: holder
})
.then((result) => {
    console.log(result)
}).catch(e => console.log(e))
```

### Transfer Token

Token holder needs to call function `transfer` to send a token to an address. 

**Example**

```text
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

You can refer to  [Transfer TRC20 script](https://gist.github.com/thanhson1085/3c831416287b0c1f4afbf9fcb3aa05dc). 

