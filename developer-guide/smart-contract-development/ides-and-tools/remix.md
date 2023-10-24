# Remix

**Remix is a Solidity IDE that’s used to write, compile and debug Solidity code.** [**Solidity**](https://solidity.readthedocs.io/) **is a high-level, contract-oriented programming language for writing smart contracts. It was influenced by popular languages such as C++, Python and JavaScript.**

IDE stands for Integrated Development Environment and is an application with a set of tools designed to help programmers execute different tasks related to software development such as writing, compiling, executing and debugging code.

Before you begin using Remix to develop smart contracts, make sure you’re familiar with some basic concepts. In particular, give these articles about [blockchain](https://www.sitepoint.com/blockchain-what-it-is-how-it-works-why-its-so-popular) and [Ethereum](https://bitfalls.com/2017/09/19/what-ethereum-compare-to-bitcoin/) a read.

#### What’s a Smart Contract/Dapp? <a href="#whatsasmartcontractdapp" id="whatsasmartcontractdapp"></a>

A smart contract is a trust-less agreement between two parties that makes use of blockchain technology, to enforce the parties to adhere to the terms, rather than relying on the traditional ways such as trusting a middleman or using laws to handle disputes.

Using the Ethereum blockchain, you can create smart contracts with the Solidity language (among others). Ethereum is not the only platform that can be used to create smart contacts, but it’s the most popular choice, as it was designed from the start to support building them.

[Dapp](http://ethdocs.org/en/latest/contracts-and-transactions/developer-tools.html#dapps) stands for _**decentralized application**_ and is a web3 application that can have a front-end written in traditional languages such as JavaScript, HTML, CSS and a smart contract (as back-end code) which runs on the blockchain. So you can simply think of a Dapp as the front end plus the associated blockchain smart contract(s).

Unlike the smart contract deployed on the blockchain itself, the front end of a Dapp can be either hosted on a centralized server like a CDN or on decentralized storage like [Swarm](http://ethdocs.org/en/latest/contracts-and-transactions/developer-tools.html#swarm).

### Accessing the Remix IDE <a href="#accessingtheremixide" id="accessingtheremixide"></a>

You can access the Remix IDE in different ways: online, via a web browser like Chrome, from a locally installed copy, or from Mist (the Ethereum Dapp browser).

#### Using the In-Browser Remix IDE <a href="#usingtheinbrowserremixide" id="usingtheinbrowserremixide"></a>

You can access the Remix IDE from your web browser without any special installation. Visit [https://remix.ethereum.org/](https://remix.ethereum.org/) and you’ll be presented with a complete IDE with a code editor and various panels for compiling, running and debugging your smart contracts. You’ll have a default example _Ballot_ contract that you can play with. Beside you should refer [Remix](https://remix-ide.readthedocs.io/en/latest/) document if need more detail.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-10-18 at 10.08.46.png" alt=""><figcaption><p>Main screen</p></figcaption></figure>

### Remix Panels <a href="#remixpanels" id="remixpanels"></a>

After seeing how to open the Remix IDE, let’s now see the various panels composing the IDE.

#### File Explorer <a href="#fileexplorer" id="fileexplorer"></a>

The file explorer provides a view with the created files stored in the browser’s storage. You can rename or delete any file by right-clicking on it, then choosing the right operation from the context menu.

![Workspace](<../../../.gitbook/assets/Screenshot 2023-10-18 at 10.32.28.png>)

Please note that the file explorer uses the browser’s local storage by default, which means you can lose all your files if you clear or the operating system automatically clears the storage. For advanced work, it’s recommended to use [Remixd](https://github.com/ethereum/remixd) - a Node.js tool (available from npm `npm install -g remixd`) which allows the Remix IDE to access your computer’s file system.

**Creating/Opening Files in Remix**

You can create a new file in the browser local storage using the first button _file_ on the top left. You can then provide a name and press Enter.

Using the second button from top left, you can open an existing Solidity file from your computer file system into the Remix IDE. The file will also be stored in the browser’s local storage.

**Publishing Explorer Files as GitHub Gists**

Using the third and fourth buttons from top left, you can publish files from the IDE as a public GitHub gist.

**Copying Files to Another Instance of Remix IDE**

Using the fifth button from top left, you can copy files from the local storage to another instance of Remix by providing the URL of the instance.

**Connecting to the Local File System**

the last button can be used to connect the Remix IDE to your local file system if you’re running the [Remixd](https://remix-ide.readthedocs.io/en/latest/remixd.html) tool.

#### Solidity Code Editor <a href="#soliditycodeeditor" id="soliditycodeeditor"></a>

The Solidity code editor provides the interface where you can write your code with many features such as syntax highlighting, auto-recompling, auto-saving etc. You can open multiple tabs and also increase/decrease the font size using the _+/-_ button in the top-left corner.

![Solidity Code Editor](<../../../.gitbook/assets/Screenshot 2023-10-18 at 10.42.36.png>)

#### Terminal <a href="#terminal" id="terminal"></a>

The terminal window below the editor integrates a JavaScript interpreter and the `web3` object. You can execute JavaScript code in the current context, visualize the actions performed from the IDE, visualize all network transactions or transactions created from the Remix IDE etc. You can also search for data in the terminal and clear the logs.

![Remix terminal](<../../../.gitbook/assets/Screenshot 2023-10-18 at 10.43.19.png>)

#### Tabs Panel <a href="#tabspanel" id="tabspanel"></a>

The _Tabs_ panel provides many tabs for working with the IDE:

* the _Compile_ tab: used for compiling a smart contract and publishing on Swarm and used for updating settings like the compiler version and many general settings for the editor.
* the _Run_ and _Deploy_ tab: used for sending transactions to the configured environment.
* the _Settings_ tab: used for updating settings like the compiler version and many general settings for the editor.
* the _Plugin_ tab: used for install local plugin in Remix.
* the _Search_ tab: used for search file which locates in Remix.
* the _File Explorer_ tab: used for display all files and folders in Remix.
* the Debug tab: used for debug when execute contract.

![Remix tabs](<../../../.gitbook/assets/Screenshot 2023-10-19 at 11.51.55.png>)

### Remix Execution Environments <a href="#remixexecutionenvironments" id="remixexecutionenvironments"></a>

The Remix IDE provides many environments for executing the transactions:

* JavaScript VM: a sandbox blockchain implemented with JavaScript in the browser to emulate a real blockchain.
* Injected Web3: a provider that injects web3 such as [`Metamask`](https://coinsbench.com/how-to-use-remix-ide-to-deploy-your-smart-contract-on-chain-5e37e1faa15a), allow you to connect to real blockchain.
* Web3 Provider: a remote node with geth, parity or any Ethereum client. Can be used to connect to the real network, or to your private blockchain directly without MetaMask in the middle.

![Remix Execution Environments](<../../../.gitbook/assets/Screenshot 2023-10-18 at 11.12.39 (1).png>)

### Using Remix IDE to Compile and Deploy a Smart Contract <a href="#usingremixidetocompileanddeployasmartcontract" id="usingremixidetocompileanddeployasmartcontract"></a>

For the sake of demonstrating what we can achieve using Remix IDE, we’ll use an example contract, and we’ll see how we can:

* Compile the contract in Remix IDE.
* See some warnings emitted by the compiler when best practices aren’t followed.
* Deploy the contract on the JavaScript EVM (Ethereum Virtual Machine).
* Make transactions on the deployed contract.
* See example reads and writes in the terminal IDE.

We’ll use the following example contract [from this tutorial](https://bitfalls.com/2018/03/31/solidity-development-crash-course-building-blockchain-raffle/) which implements a simple contract to store variable on blockchain:

```solidity
pragma solidity >=0.8.2 <0.9.0;

/**
 * @title Storage
 * @dev Store & retrieve value in a variable
 * @custom:dev-run-script ./scripts/deploy_with_ethers.ts
 */
contract Storage {

    uint256 number;

    /**
     * @dev Store value in variable
     * @param num value to store
     */
    function store(uint256 num) public {
        number = num;
    }

    /**
     * @dev Return value 
     * @return value of 'number'
     */
    function retrieve() public view returns (uint256){
        return number;
    }
}
```

Now, go ahead and open the Remix IDE from [remix.ethereum.org](https://remix.ethereum.org/).

Next, create a new file by clicking on the button with the _+_ icon.

![Create a new file](broken-reference)

And then you must enter a name , then press Enter:

![Set filename](<../../../.gitbook/assets/Screenshot 2023-10-18 at 11.25.28.png>)

A new tab will be opened in the code editor where you can start writing your contract. So just copy and paste the previous contract code in there.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-10-18 at 11.35.26.png" alt=""><figcaption><p>New blank file</p></figcaption></figure>

Next, let’s deploy the contract with our RemixVM. Switch to the _Deploy and_ _Run Transaction_ tab, and select _Remix VM_ from the dropdown menu.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-10-18 at 11.38.17.png" alt=""><figcaption><p>Deployment environments</p></figcaption></figure>

Next, click the _Deploy_ button below the contract name.

<figure><img src="broken-reference" alt=""><figcaption><p>Deploy the contract</p></figcaption></figure>

Once the contract is deployed successfully on the Remix VM, a box will be opened on the bottom as below.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-10-18 at 11.43.06.png" alt=""><figcaption><p>Contract is deployed</p></figcaption></figure>

Under the name and address of the deployed contract, we have some buttons with red and blue colors. Red buttons refer to actions that cause a write to the blockchain, where blue buttons refer to reading from blockchain.

The Remix VM provides 15 fake accounts with _100_ ether each, which we can use to test the contract. You can select a current account from the dropdown menu with the name _Account_ below the _Environment_ dropdown.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-10-18 at 11.48.03.png" alt=""><figcaption><p>Built-in account for testing</p></figcaption></figure>

You can see we have 2 functions, therefore we interact with smart contract easily. As below, we just called function store to change global variable number of contract.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-10-18 at 11.55.47.png" alt=""><figcaption><p>Call a contract</p></figcaption></figure>

After call a function in smart contract, you can check log in terminal as below:

<figure><img src="../../../.gitbook/assets/Screenshot 2023-10-18 at 13.35.40.png" alt=""><figcaption><p>Transaction log in terminal</p></figcaption></figure>

When compile contract, we might run into several errors. Therefore , Remix support developer by using ChatGPT, as you can see below:

<figure><img src="../../../.gitbook/assets/Screenshot 2023-10-19 at 11.58.25.png" alt=""><figcaption><p>ChatGPT support</p></figcaption></figure>

### Remix Alternatives <a href="#remixalternatives" id="remixalternatives"></a>

There are many alternatives for easy development and deployment of smart contracts, such as:

* [Hardhat](https://hardhat.org/hardhat-runner/docs/getting-started#overview): Hardhat is a development environment for Ethereum software. It consists of different components for editing, compiling, debugging and deploying your smart contracts and dApps, all of which work together to create a complete development environment.
* [Embark](https://github.com/embark-framework/embark): a framework that allows you to easily develop and deploy Decentralized Applications (DApps).
* [MetaMask](https://metamask.io/): a bridge that allows you to visit the distributed web of tomorrow in your browser today. It allows you to run Ethereum DApps right in your browser without running a full Ethereum node. For how to develop with MetaMask, check this [faq](https://github.com/MetaMask/faq/).
* [Dapp](https://dapp.readthedocs.io/en/latest/): Dapp is a simple command line tool for smart contract development.
* different plugins for adding Solidity support to popular IDEs such as [this Visual Code plugin](https://marketplace.visualstudio.com/items?itemName=JuanBlanco.solidity) and [this Atom plugin](https://atom.io/packages/language-ethereum) etc.

### Conclusion <a href="#conclusion" id="conclusion"></a>

We’ve introduced you to the Remix IDE for developing smart contracts for the Ethereum blockchain. You can find more detailed information in the [docs](https://remix-ide.readthedocs.io/en/latest/).

With a basic introduction behind you, feel free to dive in deeper and experiment with changing the code and exploring the different functions and tabs the editor offers.
