---
description: >-
  A basic example that sets the value of a variable and exposes it for other
  contracts to access
---

# A Simple Smart Contract

#### Storage Example

```solidity
pragma solidity 0.8.17;

contract SimpleStorage {
    uint storedData;

    function set(uint256 x) public {
        storedData = x;
    }

    function get() public view returns (uint) {
        return storedData;
    }
}
```

The first line tells you that the source code is written for Solidity version 0.8.17. This is to ensure that the contract is compatible with the current EVM version in TomoChain.

A contract in the sense of Solidity is a collection of code (its _functions_) and data (its _state_) that resides at a specific address on the TomoChain blockchain. The line `uint storedData;` declares a state variable called `storedData` of type `uint256` (unsigned integer of _256_ bits). You can think of it as a single slot in a database that you can query and alter by calling functions of the code that manages the database. In this example, the contract defines the functions `set` and `get` that can be used to modify or retrieve the value of the variable.

To access a state variable, you do not need the prefix `this` as is common in other languages.

This contract does not do much yet apart from allowing anyone to store a single number that is accessible by anyone in the world without a (feasible) way to prevent you from publishing this number. Anyone could call `set` again with a different value and overwrite your number, but the number is still stored in the history of the blockchain. Later, you will see how you can impose access restrictions so that only you can alter the number.

#### Subcurrency Example

The following contract implements the simplest form of a cryptocurrency. The contract allows only its creator to create new coins (different issuance schemes are possible). Anyone can send coins to each other without a need for registering with a username and password, all you need is a TomoChain private key.

```solidity
pragma solidity 0.8.17;

contract Coin {
    // The keyword "public" makes variables
    // accessible from other contracts
    address public minter;
    mapping (address => uint256) public balances;

    // Events allow clients to react to specific
    // contract changes you declare
    event Sent(address from, address to, uint256 amount);

    // Constructor code is only run when the contract
    // is created
    constructor() public {
        minter = msg.sender;
    }

    // Sends an amount of newly created coins to an address
    // Can only be called by the contract creator
    function mint(address receiver, uint256 amount) public {
        require(msg.sender == minter);
        require(amount < 1e60);
        balances[receiver] += amount;
    }

    // Sends an amount of existing coins
    // from any caller to an address
    function send(address receiver, uint256 amount) public {
        require(amount <= balances[msg.sender], "Insufficient balance.");
        balances[msg.sender] -= amount;
        balances[receiver] += amount;
        emit Sent(msg.sender, receiver, amount);
    }
}
```

This contract introduces some new concepts, let us go through them one by one.

The line `address public minter;` declares a state variable of type [address](https://docs.soliditylang.org/en/v0.8.17/types.html#address). The `address` type is a 160-bit value that does not allow any arithmetic operations. It is suitable for storing addresses of contracts, or a hash of the public half of a keypair belonging to [external accounts](https://docs.soliditylang.org/en/v0.8.17/introduction-to-smart-contracts.html#accounts).

The keyword `public` automatically generates a function that allows you to access the current value of the state variable from outside of the contract. Without this keyword, other contracts have no way to access the variable. The code of the function generated by the compiler is equivalent to the following (ignore `external` and `view` for now):

```solidity
function minter() external view returns (address) { return minter; }
```

You could add a function like the above yourself, but you would have a function and state variable with the same name. You do not need to do this, the compiler figures it out for you.

The next line, `mapping (address => uint256) public balances;` also creates a public state variable, but it is a more complex datatype. The [mapping](https://docs.soliditylang.org/en/v0.8.17/types.html#mapping-types) type maps addresses to [unsigned integers](https://docs.soliditylang.org/en/v0.8.17/types.html#integers).

Mappings can be seen as [hash tables](https://en.wikipedia.org/wiki/Hash\_table) which are virtually initialised such that every possible key exists from the start and is mapped to a value whose byte-representation is all zeros. However, it is neither possible to obtain a list of all keys of a mapping, nor a list of all values. Record what you added to the mapping or use it in a context where this is not needed. Or even better, keep a list, or use a more suitable data type.

The [getter function](https://docs.soliditylang.org/en/v0.8.17/contracts.html#getter-functions) created by the `public` keyword is more complex in the case of a mapping. It looks like the following:

```solidity
function balances(address _account) external view returns (uint256) {
    return balances[_account];
}
```

You can use this function to query the balance of a single account.

The line `event Sent(address from, address to, uint256 amount);` declares an [“event”](https://solidity.readthedocs.io/en/v0.6.3/contracts.html#events), which is emitted in the last line of the function `send`. TomoChain clients such as web applications can listen for these events emitted on the blockchain without much cost. As soon as it is emitted, the listener receives the arguments `from`, `to` and `amount`, which makes it possible to track transactions.

To listen for this event, you could use the following JavaScript code, which uses [web3.js](https://github.com/ethereum/web3.js/) to create the `Coin` contract object, and any user interface calls the automatically generated `balances` function from above:

```javascript
Coin.Sent().watch({}, '', function(error, result) {
    if (!error) {
        console.log("Coin transfer: " + result.args.amount +
            " coins were sent from " + result.args.from +
            " to " + result.args.to + ".");
        console.log("Balances now:\n" +
            "Sender: " + Coin.balances.call(result.args.from) +
            "Receiver: " + Coin.balances.call(result.args.to));
    }
})
```

The [constructor](https://docs.soliditylang.org/en/v0.8.17/contracts.html#constructor) is a special function run during the creation of the contract and cannot be called afterwards. In this case, it permanently stores the address of the person creating the contract. The `msg` variable (together with `tx` and `block`) is a [special global variable](https://docs.soliditylang.org/en/v0.8.17/units-and-global-variables.html#special-variables-functions) that contains properties which allow access to the blockchain. `msg.sender` is always the address where the current (external) function call came from.

The functions that make up the contract, and that users and contracts can call are `mint` and `send`.

The `mint` function sends an amount of newly created coins to another address. The [require](https://docs.soliditylang.org/en/v0.8.17/control-structures.html#assert-and-require) function call defines conditions that reverts all changes if not met. In this example, `require(msg.sender == minter);` ensures that only the creator of the contract can call `mint`, and `require(amount < 1e60);` ensures a maximum amount of tokens. This ensures that there are no overflow errors in the future.

The `send` function can be used by anyone (who already has some of these coins) to send coins to anyone else. If the sender does not have enough coins to send, the `require` call fails and provides the sender with an appropriate error message string.