# Write the Smart Contract

We’ll start our Dapp by writing the smart contract that acts as the back-end logic and storage.

1. Create a new file named `Adoption.sol` in the `contracts/` directory.
2. Copy the following code:

```text
pragma solidity ^0.5.0;contract Adoption {
  address[16] public adopters;  // Adopting a pet
  function adopt(uint petId) public returns (uint) {
    // check that petId is in range of our adopters array
    require(petId >= 0 && petId <= 15);    // add the address who called this function to our adopter array
    adopters[petId] = msg.sender;    // return the petId provided as a confirmation
    return petId;
  }  // Retrieving the adopters
  function getAdopters() public view returns (address[16] memory) {
    return adopters;
  }
}
```

> **Note:** Code from [Truffle’s Pet-Shop tutorial](https://truffleframework.com/tutorials/pet-shop#writing-the-smart-contract) — if you want to look deeper into the Solidity code, they slowly go through the Truffle link explaining the details.



## Compiling <a id="df38"></a>

Solidity is a compiled language, meaning we need to compile our Solidity to bytecode for the **Ethereum Virtual Machine \(EVM\)** to execute. Think of it as translating our human-readable Solidity into something the EVM understands.

> TomoChain is EVM-compatible, which means that every contract written in Ethereum can be seamlessly ported to TomoChain without effort

In a terminal, make sure you are in the root of the directory that contains the Dapp and type:

```text
truffle compile
```

You should see output similar to the following:

```text
Compiling ./contracts/Migrations.sol... 
Compiling ./contracts/Adoption.sol... 
Writing artifacts to ./build/contracts
```

