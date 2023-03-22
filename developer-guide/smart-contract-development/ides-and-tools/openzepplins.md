# Openzepplins

OpenZeppelin ([https://openzeppelin.org](https://openzeppelin.org/)) is an amazing library of well documented smart contracts for Solidity development. You will find its contracts helpful for many of your projects.

The most obvious use of OpenZeppelin is its implementations of ERC-20 and ERC-721 tokens. But there is a lot more here that can save us from reinventing the wheel. There are contracts for access control, crowdsales, and escrow payments — just to name a few.

Truffle ([https://truffleframework.com](https://truffleframework.com/docs/truffle/overview)) is a development framework you can use for Solidity projects. It makes your life easier in a lot of ways; but the biggest value add is how it helps you test your contracts.

Right out of the box, Truffle lets you compile and migrate your contracts to a local test network. From there you can either use the Truffle console to manually interact with the deployed contracts, or run unit tests written in Javascript with Mocha and Chai.

## **Installation** <a href="#96e5" id="96e5"></a>

First we install Truffle (requires Node.js v8.9.4 or later):

```
npm install -g truffle
```

Next we use Truffle to initialize a new project for us:

```
mkdir MyProject && cd MyProject
truffle init
```

Now we install OpenZeppelin in our new project:

```
npm init -y
npm install --save-exact openzeppelin-solidity
```

We use `--save-exact` because minor version updates to OpenZeppelin can introduce breaking changes.

## **Configure Solidity compiler** <a href="#869a" id="869a"></a>

OpenZeppelin contracts require the Solidity 0.5.2 compiler (solc), but Truffle ships with solc 0.5.0 by default. If we want to use OpenZeppelin with our own contracts, we must configure Truffle to use 0.5.2.

Let’s add the following to `./truffle-config.js`:

```
module.exports = {
  compilers: {
    solc: {
      version: “0.5.2”
    }
  }
}
```

Do not worry about installing the correct compiler version manually. Truffle will download it automatically with this configuration.

## Write Smart Contracts <a href="#4600" id="4600"></a>

When you initialize a project with Truffle, it creates a `./contracts` directory for your Solidity source code. Inside you will see `Migrations.sol` which is used to manage your contract migrations, so don’t delete it.

Any contract created inside this directory will be automatically detected by Truffle.

## **Import OpenZeppelin libraries** <a href="#fb2c" id="fb2c"></a>

Once you start writing your own Solidity smart contracts, using OpenZeppelin is easy. Because Truffle understands NPM packages, Solidity libraries installed to `./node_modules` are readily available without any configuration.

For example, importing OpenZeppelin’s ERC-20 implementation is as simple as:

```
import 'openzeppelin-solidity/contracts/token/ERC20/ERC20.sol';
```

## **Deploy with Truffle** <a href="#f87a" id="f87a"></a>

Truffle’s deployment process is versatile, but if all we want to do is test any smart contracts we’ve created, it couldn’t be more straightforward.

Open the Truffle console with:

```
truffle develop
```

This automatically connects to Truffle’s built-in local test network.

In the console we run `compile` and then `migrate`. Compilation generates the contract bytecode and application binary interface (ABI). Migration sends transactions to the network that create instances of our smart contracts.

The Truffle console also exposes contract abstractions and web3.js if we want to manually interact with our contracts after deployment.

For example, if we have an ERC-20 token contract called `MyToken`, we could find out the total supply with:

```
const instance = await MyToken.deployed()
instance.totalSupply()
```

## **Where to go from here** <a href="#26a2" id="26a2"></a>

We recommend looking through the OpenZeppelin documentation ([docs.openzeppelin.org/docs/get-started.html](https://docs.openzeppelin.com/contracts/2.x/)) to see how your projects can benefit from its library of smart contracts.
