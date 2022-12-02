# Remix

**Remix is a Solidity IDE that’s used to write, compile and debug Solidity code.** [**Solidity**](https://solidity.readthedocs.io/) **is a high-level, contract-oriented programming language for writing smart contracts. It was influenced by popular languages such as C++, Python and JavaScript.**

IDE stands for Integrated Development Environment and is an application with a set of tools designed to help programmers execute different tasks related to software development such as writing, compiling, executing and debugging code.

Before you begin using Remix to develop smart contracts, make sure you’re familiar with some basic concepts. In particular, give these articles about [blockchain](https://www.sitepoint.com/blockchain-what-it-is-how-it-works-why-its-so-popular) and [Ethereum](https://bitfalls.com/2017/09/19/what-ethereum-compare-to-bitcoin/) a read.

#### What’s a Smart Contract/Dapp? <a href="#whatsasmartcontractdapp" id="whatsasmartcontractdapp"></a>

A smart contract is a trust-less agreement between two parties that makes use of blockchain technology, to enforce the parties to adhere to the terms, rather than relying on the traditional ways such as trusting a middleman or using laws to handle disputes.

Using the Ethereum blockchain, you can create smart contracts with the Solidity language (among others). Ethereum is not the only platform that can be used to create smart contacts, but it’s the most popular choice, as it was designed from the start to support building them.

[Dapp](http://ethdocs.org/en/latest/contracts-and-transactions/developer-tools.html#dapps) stands for _**de**_**centralized **_**app**_**lication** and is a web3 application that can have a front-end written in traditional languages such as JavaScript, HTML, CSS and a smart contract (as back-end code) which runs on the blockchain. So you can simply think of a Dapp as the front end plus the associated blockchain smart contract(s).

Unlike the smart contract deployed on the blockchain itself, the front end of a Dapp can be either hosted on a centralized server like a CDN or on decentralized storage like [Swarm](http://ethdocs.org/en/latest/contracts-and-transactions/developer-tools.html#swarm).

### Accessing the Remix IDE <a href="#accessingtheremixide" id="accessingtheremixide"></a>

You can access the Remix IDE in different ways: online, via a web browser like Chrome, from a locally installed copy, or from Mist (the Ethereum Dapp browser).

#### Using the In-Browser Remix IDE <a href="#usingtheinbrowserremixide" id="usingtheinbrowserremixide"></a>

You can access the Remix IDE from your web browser without any special installation. Visit [https://remix.ethereum.org/](https://remix.ethereum.org/) and you’ll be presented with a complete IDE with a code editor and various panels for compiling, running and debugging your smart contracts. You’ll have a default example _Ballot_ contract that you can play with.

![Remix IDE](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528071944remix-ide-1024x780.png)

#### Starting Remix IDE from Mist <a href="#startingremixidefrommist" id="startingremixidefrommist"></a>

You can start the Remix IDE from Mist by clicking on _Develop_, then _Open Remix IDE_. Remix will be opened in a new window. If this is your first time running the IDE, you’ll be presented with a simple example _Ballot_ contract.

To get familiar with Mist, please see [this article](https://bitfalls.com/2018/02/12/explaining-ethereum-tools-geth-mist/).

#### Running your Own Copy of Remix IDE <a href="#runningyourowncopyofremixide" id="runningyourowncopyofremixide"></a>

You can also run your own copy of Remix IDE by executing the following commands:

```
npm install remix-ide -g
remix-ide
```

You need to have Node.js and npm installed. Check this [GitHub repository](https://github.com/ethereum/remix-ide) for more information.

### Remix Panels <a href="#remixpanels" id="remixpanels"></a>

After seeing how to open the Remix IDE, let’s now see the various panels composing the IDE.

#### File Explorer <a href="#fileexplorer" id="fileexplorer"></a>

The file explorer provides a view with the created files stored in the browser’s storage. You can rename or delete any file by right-clicking on it, then choosing the right operation from the context menu.

![context menu options](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528072165rename-delete.png)

Please note that the file explorer uses the browser’s local storage by default, which means you can lose all your files if you clear or the operating system automatically clears the storage. For advanced work, it’s recommended to use [Remixd](https://github.com/ethereum/remixd) — a Node.js tool (available from npm `npm install -g remixd`) which allows the Remix IDE to access your computer’s file system.

Now let’s see the different actions that you can perform using the buttons at the top of the explorer.

![Remix buttons](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528072282remix-buttons.png)

**Creating/Opening Files in Remix**

You can create a new file in the browser local storage using the first button with the `+` icon on the top left. You can then provide a name in the opened dialog and press _OK_.

Using the second button from top left, you can open an existing Solidity file from your computer file system into the Remix IDE. The file will also be stored in the browser’s local storage.

**Publishing Explorer Files as GitHub Gists**

Using the third and fourth buttons from top left, you can publish files from the IDE as a public GitHub gist.

**Copying Files to Another Instance of Remix IDE**

Using the fifth button from top left, you can copy files from the local storage to another instance of Remix by providing the URL of the instance.

**Connecting to the Local File System**

The last button can be used to connect the Remix IDE to your local file system if you’re running the Remixd tool.

#### Solidity Code Editor <a href="#soliditycodeeditor" id="soliditycodeeditor"></a>

The Solidity code editor provides the interface where you can write your code with many features such as syntax highlighting, auto-recompling, auto-saving etc. You can open multiple tabs and also increase/decrease the font size using the _+/-_ button in the top-left corner.

![Solidity Code Editor](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528072494solidity-code-editor.png)

#### Terminal <a href="#terminal" id="terminal"></a>

The terminal window below the editor integrates a JavaScript interpreter and the `web3` object. You can execute JavaScript code in the current context, visualize the actions performed from the IDE, visualize all network transactions or transactions created from the Remix IDE etc. You can also search for data in the terminal and clear the logs.

![Remix terminal](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528072582remix-terminal.png)

#### Tabs Panel <a href="#tabspanel" id="tabspanel"></a>

The _Tabs_ panel provides many tabs for working with the IDE:

* the _Compile_ tab: used for compiling a smart contract and publishing on Swarm
* the _Run_ tab: used for sending transactions to the configured environment
* the _Settings_ tab: used for updating settings like the compiler version and many general settings for the editor
* the _Debugger_ tab: used for debugging transactions
* the _Analysis_ tab: used for getting information about the latest compilation
* the _Support_ tab: used for connecting with the Remix community.

![Remix tabs](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528072805remix-tabs.png)

### Remix Execution Environments <a href="#remixexecutionenvironments" id="remixexecutionenvironments"></a>

The Remix IDE provides many environments for executing the transactions:

* JavaScript VM: a sandbox blockchain implemented with JavaScript in the browser to emulate a real blockchain.
* Injected Web3: a provider that injects web3 such as `Mist` and `Metamask`, [connecting you to your private blockchain](https://bitfalls.com/2018/03/26/connecting-myetherwallet-mist-metamask-private-blockchain/).
* Web3 Provider: a remote node with geth, parity or any Ethereum client. Can be used to connect to the real network, or to your private blockchain directly without MetaMask in the middle.

![Remix Execution Environments](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528072980remix-execution-environments.png)

### Using Remix IDE to Compile and Deploy a Smart Contract <a href="#usingremixidetocompileanddeployasmartcontract" id="usingremixidetocompileanddeployasmartcontract"></a>

For the sake of demonstrating what we can achieve using Remix IDE, we’ll use an example contract and we’ll see how we can:

* compile the contract in Remix IDE
* see some warnings emitted by the compiler when best practices aren’t followed
* deploy the contract on the JavaScript EVM (Ethereum Virtual Machine)
* make transactions on the deployed contract
* see example reads and writes in the terminal IDE.

We’ll use the following example contract [from this tutorial](https://bitfalls.com/2018/03/31/solidity-development-crash-course-building-blockchain-raffle/) which implements a blockchain raffle:

```
pragma solidity ^0.4.20;

contract Blocksplit {

    address[] public players;
    mapping (address => bool) public uniquePlayers;
    address[] public winners;

    address public charity = 0xc39eA9DB33F510407D2C77b06157c3Ae57247c2A;

    function() external payable {
        play(msg.sender);
    }

    function play(address _participant) payable public {
        require (msg.value >= 1000000000000000 && msg.value <= 100000000000000000);
        require (uniquePlayers[_participant] == false);

        players.push(_participant);
        uniquePlayers[_participant] = true;
    }

}
```

The contract declares some variables, such as:

* The `players` array variable, which holds the addresses of the raffle participants.
* The `uniquePlayers` mapping, which is used to save unique players so players don’t participate multiple times from the same address. (An address will be mapped to a boolean, true or false, value indicating if the participant has already participated or not.)
* The `winners` array variable, which will hold the addresses of the winners.
* The `charity` variable, which holds a hardcoded address of a charity where profits will go.

It also declares:

* A fallback function marked as `payable`, which enables the smart contract to accept payments.
* A `play()` function that enables participants to enter the raffle by providing an address.

You can read more details about this contract from this [tutorial](https://bitfalls.com/2018/03/31/solidity-development-crash-course-building-blockchain-raffle/) where all the code is explained in detail.

Now, go ahead and open the Remix IDE from [remix.ethereum.org](https://remix.ethereum.org/).

Next, create a new file by clicking on the button with the _+_ icon.

![Creating a new file](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528073262remix-buttons1.png)

A new dialog will pop up Enter a name for your file (`blocksplit.sol`), then press _OK_:

![Naming the file](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528073351naming-file.png)

A new tab will be opened in the code editor where you can start writing your contract. So just copy and paste the previous contract code in there.

First start by compiling the contract. From the _Compile_ tab click _Start to compile_ button.

We’re getting a message box with two warnings raised by Static Analysis of the code.

![Two warnings](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528073432two-warnings.png)

If you click on the message box you’ll be taken to the _Analysis_ tab, which provides more information about the warnings:

![warning info](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528073508warning-info.png)

The first warning is raised if the gas requirements of functions are too high, and the second one is raised if the `require()` or `assert()` functions are not used appropriately.

You can also use the checkboxes in the _Analysis_ tab to determine when you want the compiler to emit warnings.

![determine when you want the compiler to emit warnings](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528073628when-to-warn.png)

Next, let’s deploy the contract with our JavaScript VM. Switch to the _Run_ tab, and select _JavaScript VM_ from the dropdown menu.

![Selecting the JavaScript VM](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528073689js-vm.png)

Next, click the _Deploy_ button below the contract name.

![The Deploy button](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528073758deploy.png)

Once the contract is deployed successfully on the JavaScript VM, a box will be opened on the bottom of the _Run_ tab.

![Run tab box](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528073835run-tab-box.png)

Under the name and address of the deployed contract, we have some buttons with red and blue colors. Red buttons refer to actions that cause a write to the blockchain (in our case the fallback and play functions) and need a transaction, where blue buttons refer to reading from blockchain (_charity, players, uniquePlayers and winners_ public variables we defined in the contract’s code).

You’ll also see a similar message to the following screenshot in the IDE terminal.

![Terminal message](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528073924terminal-message.png)

For now, the only variable that holds a value is the _charity_ variable, because the address is hardcoded in the code so if you click on the corresponding button you’ll get the value of that address.

![address value](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528074002address-value.png)

The contract is built to allow a participant to enter the raffle by just sending ether to the address (using a payable callback function) or also call the `play()` function with the address of the participant.

The JavaScript VM provides five fake accounts with _100_ ether each, which we can use to test the contract. You can select a current account from the dropdown menu with the name _Account_ below the _Environment_ dropdown.

![Select a current account](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528074083select-account.png)

Now, to send money to the contract, we first set the _Value_ variable (between 0.001 and 0.1) and the unit (ether) from the dropdown menu. Then we call the fallback function by simply clicking on its corresponding red button.

![Calling the fallback function](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528074156calling-fallback.png)

That’s it. We’ve sent money to the contract. The address of the selected account should be added to the `players` array. To check that, simply click on the blue _players_ button.

![Clicking on the blue Players button](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528074260players-button.png)

You can add other participants by selecting a new account and repeat the previous process (to check if an account is added to the array simply enter the index, from 0 to 4, for that account in the text-box next to _players_ button).

If you add an account that has already participated, you should get a warning in the terminal and the transaction will fail with a message like the following:

![Failure message](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2018/06/1528074354failure-message.png)

### Remix Alternatives <a href="#remixalternatives" id="remixalternatives"></a>

There are many alternatives for easy development and deployment of smart contracts, such as:

* [Truffle](http://truffleframework.com/): advertised as the Ethereum Swiss army knife and claims to be the most popular development framework for Ethereum with a mission to make your life a whole lot easier. We’ll be working with Truffle a lot in upcoming tutorials.
* [Embark](https://github.com/embark-framework/embark): a framework that allows you to easily develop and deploy Decentralized Applications (DApps).
* [MetaMask](https://metamask.io/): a bridge that allows you to visit the distributed web of tomorrow in your browser today. It allows you to run Ethereum DApps right in your browser without running a full Ethereum node. For how to develop with MetaMask, check this [faq](https://github.com/MetaMask/faq/).
* [Dapp](https://dapp.readthedocs.io/en/latest/): Dapp is a simple command line tool for smart contract development.
* different plugins for adding Solidity support to popular IDEs such as [this Visual Code plugin](https://marketplace.visualstudio.com/items?itemName=JuanBlanco.solidity) and [this Atom plugin](https://atom.io/packages/language-ethereum) etc.

### Conclusion <a href="#conclusion" id="conclusion"></a>

We’ve introduced you to the Remix IDE for developing smart contracts for the Ethereum blockchain. You can find more detailed information in the [docs](http://remix.readthedocs.io/en/latest/).

With a basic introduction behind you, feel free to dive in deeper and experiment with changing the code and exploring the different functions and tabs the editor offers.
