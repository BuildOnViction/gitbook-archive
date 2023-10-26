---
description: >-
  This page is a reduced version of the Solidity docs site that is adapted to
  TomoChain network to avoid overwhelming information.
---

# Solidity

### About

Solidity is a contract-oriented, high-level language for implementing smart contracts. It was influenced by Python and JavaScript and is designed to target the Ethereum Virtual Machine (EVM) both Ethereum and TomoChain.

Solidity is statically typed, supports inheritance, libraries and complex user-defined types among other features.

### Solidity in TomoChain

TomoChain support Solidity compiler version **<=0.8.17**, which targets `London` hardfork in Ethereum. However, due the fee mechanism in TomoChain, `BASEFEE` opcode is unused and not supported by the runtime.

{% hint style="info" %}
For Solidity compiler version >=0.8.18, you may still compile and deploy to TomoChain. However, use it at your own risk.
{% endhint %}

The table below describes all the opcodes that isn't available in TomoChain:

<table><thead><tr><th width="143.5">Opcode</th><th>Description</th></tr></thead><tbody><tr><td>BASEFEE</td><td>Return base fee of block, this using for <a href="https://eips.ethereum.org/EIPS/eip-1559">https://eips.ethereum.org/EIPS/eip-1559</a> on London hardfork.</td></tr><tr><td>TLOAD</td><td>This opcode using for Access List Transaction Type, which hasn’t have any implement for now</td></tr><tr><td>TSTORE</td><td>This opcode using for Access List Transaction Type</td></tr><tr><td>PUSH0</td><td>This opcode pushes the constant value 0 onto the stack. It is generated in Solidity version 0.8.20 or higher.</td></tr><tr><td>INVALID</td><td>Improve the traces process.</td></tr><tr><td>BLOBHASH</td><td>Which is specific to DankSharing hardfork.</td></tr></tbody></table>

### Example

As you will see, it is possible to create contracts for voting, crowdfunding, blind auctions, multi-signature wallets and more.

{% hint style="info" %}
The best way to try out Solidity right now is using [Remix](https://remix.ethereum.org/) (it can take a while to load, please be patient). Remix is a web browser-based IDE that allows you to write Solidity smart contracts, then deploy and run the smart contracts.
{% endhint %}

Once you're strong enough, on the next pages, we will first see a [simple smart contract](https://docs.soliditylang.org/en/v0.8.17/introduction-to-smart-contracts.html#simple-smart-contract) written in Solidity followed by the basics about [blockchains](https://docs.soliditylang.org/en/v0.8.17/introduction-to-smart-contracts.html#blockchain-basics) and the [Ethereum Virtual Machine](https://docs.soliditylang.org/en/v0.8.17/introduction-to-smart-contracts.html#the-ethereum-virtual-machine).

The next section will explain several _features_ of Solidity by giving useful [example contracts](https://docs.soliditylang.org/en/v0.8.17/solidity-by-example.html#voting). Remember that you can always try out the contracts [in your browser](https://remix.ethereum.org/)!

The last and most extensive section will cover all aspects of Solidity in depth.

If you still have questions, you can try searching or asking on the [Ethereum Stackexchange](https://ethereum.stackexchange.com/) site, or come to our [Gitter channel](https://gitter.im/ethereum/solidity/). Ideas for improving Solidity or this documentation are always welcome! the world:

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}
