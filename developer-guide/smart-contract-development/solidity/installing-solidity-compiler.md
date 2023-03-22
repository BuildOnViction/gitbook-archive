# Installing Solidity compiler

### Versioning

Solidity versions follow [semantic versioning](https://semver.org/) and in addition to releases, **nightly development builds** are also made available. However, we recommend to only install Solidity compiler versions <= 0.5.0 as higher versions introduce breaking changes resulting in opcodes that are not available in that current EVM version of TomoChain. &#x20;

### Remix

_We recommend Remix for small contracts and for quickly learning Solidity._

[Access Remix online](https://remix.ethereum.org/), you do not need to install anything. If you want to use it without connection to the Internet, go to [https://github.com/ethereum/remix-live/tree/gh-pages](https://github.com/ethereum/remix-live/tree/gh-pages) and download the `.zip` file as explained on that page. Remix is also a convenient option for testing nightly builds without installing multiple Solidity versions.

Further options on this page detail installing commandline Solidity compiler software on your computer. Choose a commandline compiler if you are working on a larger contract or if you require more compilation options.

To use Remix with TomoChain, you only need to connect your Metamask to TomoChain using TomoChain's RPC and following [this tutorial](../../../general/how-to-connect-to-tomochain-network/metamask.md).

### npm / Node.js

Use npm for a convenient and portable way to install solcjs, a Solidity compiler. The solcjs program has fewer features than the ways to access the compiler described further down this page. The [Using the Commandline Compiler](https://solidity.readthedocs.io/en/v0.6.3/using-the-compiler.html#commandline-compiler) documentation assumes you are using the full-featured compiler, solc. The usage of solcjs is documented inside its own [repository](https://github.com/ethereum/solc-js).

Note: The solc-js project is derived from the C++ solc by using Emscripten which means that both use the same compiler source code. solc-js can be used in JavaScript projects directly (such as Remix). Please refer to the solc-js repository for instructions.

```
npm install -g solc
```
