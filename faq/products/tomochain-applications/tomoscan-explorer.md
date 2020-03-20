# TomoScan \(Explorer\)

## **General Questions**  

### **What is TomoScan?**

[TomoScan](https://scan.tomochain.com/) is a block explorer for TomoChain. It is pretty similar to EtherScan used on the Ethereum network if you are already familiar with it.

TomoScan provides a user-friendly interface to explore the TomoChain blockchain. From a user perspective, TomoScan provides transparency because all block information, transactions, finality, smart contracts, Dapps and token information are read from TomoChain and displayed here. Furthermore, TomoScan offers technical visualisations and useful statistics about TomoChain performance, token holders and other functionalities.

### **What is a TxHash? How to check a TxHash?**

TxHash stands for 'transaction hash', and is also known as a transaction ID.

An example of what a TxHash looks like: `0xedab9e59d4567e9ced8d61caefe20e1e2a3fe95cceaaeabc98466ef3f03c0eca`

To check a TxHash, follow the steps below:

On [TomoScan](https://scan.tomochain.com/), go to the search bar with the magnifying glass icon. Paste your transaction hash \(TxHash\) in the search bar and click the icon or press ENTER. Your transaction details will show up.

Example: [https://scan.tomochain.com/txs/0xedab9e59d4567e9ced8d61caefe20e1e2a3fe95cceaaeabc98466ef3f03c0eca](https://scan.tomochain.com/txs/0xedab9e59d4567e9ced8d61caefe20e1e2a3fe95cceaaeabc98466ef3f03c0eca)

## Features 

### [Home](https://scan.tomochain.com/)

![TomoScan homepage](../../../.gitbook/assets/tomoscan1.jpg)

This is the home page of TomoScan. In the middle of the page you can find a search field that lets you find anything by its address. Under it, some general stats gives you the total amount of accounts, tokens, contracts and blocks.

### [Transactions](https://scan.tomochain.com/txs) <a id="transactions"></a>

![](../../../.gitbook/assets/tomoscan2.jpg)

When consulting a single transaction, the page lists the following information: - The transaction's ID \(Transaction Hash\). - The transaction status. - The transaction containing block. - The transaction age. - The transaction sender address. - The transaction recipient address. - The transaction amount in TOMO. - The transaction gas used. - The transaction gas price. - The transaction total gas cost. - The transaction data.

#### [All transactions](https://scan.tomochain.com/txs) <a id="all-transactions"></a>

All the transactions that happened on the chain.

#### [Signed transactions](https://scan.tomochain.com/txs/signTxs) <a id="sign-transactions"></a>

Signed transactions emitted by the Masternodes.

#### [Pending transactions](https://scan.tomochain.com/txs/pending) <a id="pending-transactions"></a>

Transactions that are not yet confirmed.

#### [Other Transactions](https://docs.tomochain.com/products/tomoscan/features/) <a id="other-transactions"></a>

All the transactions minus the sign and pending ones.

### [Accounts](https://scan.tomochain.com/accounts) <a id="accounts"></a>

![](../../../.gitbook/assets/tomoscan3.jpg)

When clicking on an account, the following information is displayed: - The account balance in TOMO. - The TOMO USD Value. - The account transactions count. - The transactions of this account. - The mined blocks. - The events of this account. - The rewards of the account for each epoch.

List of accounts on TomoChain.

#### [All accounts](https://scan.tomochain.com/accounts) <a id="all-accounts"></a>

All the accounts that exist on the chain. The page lists the following information: - The account rank \(ordered by balance\). - The account address. - The account balance in TOMO. - The account transaction count.

#### [All Masternodes](https://scan.tomochain.com/masternodes) <a id="all-masternodes"></a>

All the Masternode accounts that exist on the chain. The page lists the following information: - The account address. - The account linked to the Masternode name. - The account linked to the Masternode owner. - The account linked to the Masternode status. - The account linked to the Masternode's latest signed block.

#### [Verified Contracts](https://scan.tomochain.com/contracts) <a id="verified-contracts"></a>

All the verified contracts that exist on-chain. A contract has to be manually verified by its owner to appear here. The page lists the following information: - The account address. - The account contract name. - The account balance in TOMO. - The account transactions count. - The account contract verification date.

### [Tokens](https://scan.tomochain.com/tokens) <a id="tokens"></a>

![](../../../.gitbook/assets/tomoscan4.jpg)

List of tokens on TomoChain including TRC20, TRC21 and TRC721, and their transfers.

#### [All Tokens](https://scan.tomochain.com/tokens) <a id="all-tokens"></a>

All the tokens on the chain. The page lists the following information: - The token address \(hash\). - The token name. - The token symbol. - The token total supply. - The token decimals. - The token transactions count.

#### [Tokens transfers](https://scan.tomochain.com/tokentxs) <a id="tokens-transfers"></a>

All the tokens transfers on the chain. The page lists the following information: - The transaction hash. - The transaction age. - The transaction sender address. - The transaction recipient address. - The transaction value in token. - The token name.

#### [Token](https://scan.tomochain.com/tokens/0x8602ce2124f9b05dc6654230079dd31250292bd5) <a id="token"></a>

When clicking on a token, the following information is displayed: - The token name. - The number of token holders. - The number of transfers made with the token. - The link of the official site, please keep in mind that TomoScan is constantly updating. Some links might be missing. - The official contract address. - Number of decimals. - Useful links. - "Filtered by": use it if you want to see a the transactions of an adsress in particular. In this example, you can check all the transactions made of the BigBom tokens from an adsress to another.

### [Blocks](https://scan.tomochain.com/blocks) <a id="blocks"></a>

![](../../../.gitbook/assets/tomoscan5.jpg)

List of all blocks on TomoChain. The page lists the following information: - The block height \(index\). - The block age. - The block number of transactions. - The block creator. - The block total gas used. - The block finality.

#### Finality

The percentage of the network which validated this block. When it reaches 75%, the block has reached its finality state and is added permanently to the chain.

### [Block](https://scan.tomochain.com/blocks/200000) <a id="block"></a>

When consulting a single block, the page lists the following information: - The block height \(index\). - The block age. - The block number of transactions. - The block hash. - The block parent hash. - The block creator address. - The block finality. - The block total gas used. - The global pre-block gas limit. - The block extra data.

A tab "Transactions" contains the list of transactions in this block. A tab "Signers" contains the list of Masternodes which signed this block.

### [Login and Registration](https://docs.tomochain.com/products/tomoscan/features/) <a id="login-and-register"></a>

If you register, you will be able to keep a watchlist of some addresses you are interested into. You will receive an email notification when this address performs actions.

Please keep in mind that TomoScan is subject to go through some changes. This is why your feedback is much appreciated!  


