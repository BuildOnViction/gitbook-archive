# Write the Smart Contract

We’ll start our Dapp by writing the smart contract that acts as the back-end logic and storage.

{% hint style="info" %}
You might have heard about ERC-20, which is a token standard in Ethereum. Tokens such as DAI and USDC implement the ERC-20 standard which allows them all to be compatible with any software that can deal with ERC-20 tokens. For the sake of simplicity, the token we're going to build does _not_ implement the ERC-20 standard.
{% endhint %}

1. Create a new file named `Token.sol` in the `contracts/` directorynote
2. Copy the following code:

```solidity
// Solidity files have to start with this pragma.
// It will be used by the Solidity compiler to validate its version.
pragma solidity ^0.8.0;


// This is the main building block for smart contracts.
contract Token {
    // Some string type variables to identify the token.
    string public name = "My Hardhat Token";
    string public symbol = "MHT";

    // The fixed amount of tokens, stored in an unsigned integer type variable.
    uint256 public totalSupply = 1000000;

    // An address type variable is used to store ethereum accounts.
    address public owner;

    // A mapping is a key/value map. Here we store each account's balance.
    mapping(address => uint256) balances;

    // The Transfer event helps off-chain applications understand
    // what happens within your contract.
    event Transfer(address indexed _from, address indexed _to, uint256 _value);

    /**
     * Contract initialization.
     */
    constructor() {
        // The totalSupply is assigned to the transaction sender, which is the
        // account that is deploying the contract.
        balances[msg.sender] = totalSupply;
        owner = msg.sender;
    }

    /**
     * A function to transfer tokens.
     *
     * The `external` modifier makes a function *only* callable from *outside*
     * the contract.
     */
    function transfer(address to, uint256 amount) external {
        // Check if the transaction sender has enough tokens.
        // If `require`'s first argument evaluates to `false` then the
        // transaction will revert.
        require(balances[msg.sender] >= amount, "Not enough tokens");

        // Transfer the amount.
        balances[msg.sender] -= amount;
        balances[to] += amount;

        // Notify off-chain applications of the transfer.
        emit Transfer(msg.sender, to, amount);
    }

    /**
     * Read only function to retrieve the token balance of a given account.
     *
     * The `view` modifier indicates that it doesn't modify the contract's
     * state, which allows us to call it without executing a transaction.
     */
    function balanceOf(address account) external view returns (uint256) {
        return balances[account];
    }
}
```

{% hint style="info" %}
The source code above is just an example to illustrate how your source code looks like. In practice, your source code may contain one or many files with complex structure.
{% endhint %}

## Compiling <a href="#df38" id="df38"></a>

Solidity is a compiled language, meaning we need to compile our Solidity to bytecode for the **Ethereum Virtual Machine (EVM)** to execute. Think of it as translating our human-readable Solidity into something the EVM understands.

> TomoChain is EVM-compatible, which means that every contract written in Ethereum can be seamlessly ported to TomoChain without effort.

To compile the contract run `npx hardhat compile` in your terminal. The `compile` task is one of the built-in tasks.

```bash
npx hardhat compile
```

You should see output similar to the following:

```bash
$ npx hardhat compile
Compiling 1 file with 0.8.17
Compilation finished successfully
```
