# An Overview of the Token Standards on TomoChain

## **Overview**

In every blockchain ecosystem the token functions as the central element of a new type of economy. A token standard defines a set of rules that governs its issuance and use.

You may be familiar with ERC (Ethereum Request for Comments), which is a technical standard used for smart contracts on the Ethereum. This terminology is the origin of TRC tokens — the equivalent of ERC on TomoChain.

### **Fungible and Non-fungible token**

There are three token standards on TomoChain so far, each with its own unique function including TRC20, TRC25, and TRC721. These token standards can be divided into two different categories: fungible and non-fungible tokens. Fungible tokens are all equal and divisible, non-fungible tokens (NFTs) are all distinct and non-divisible.

Non-fungible tokens of the type TRC721 are those that represent a unique asset, like a certificate or a collectible in-game item. Fungible tokens are interchangeable and can be divided into smaller token units like TOMO. The fungible token standard includes TRC20 and TRC25 as digital assets used to offer access to products and/or services on a platform. The table below compares the differences between three types of token standards on TomoChain.

|                                                 | **TRC721**        | **TRC25**                | **TRC20**     |
| ----------------------------------------------- | ----------------- | ------------------------ | ------------- |
| **Divisibility**                                | **Non-Divisible** | **Divisible**            | **Divisible** |
| **Technical requirements for Dapp integration** | **Moderate**      | **Moderate**             | **Low**       |
| **Technical requirements for exchange listing** | **N/A**           | **Moderate**             | **Low**       |
| **Transaction Fee**                             | **In TOMO**       | **In Transaction Token** | **In TOMO**   |

### **TRC20 - Easy integration**

TRC20 is an equivalent token standard of ERC20 built on top of the TomoChain blockchain. TRC20 token holders would need to hold a small amount of TOMO to cover the extremely low transaction fees.

TRC20 wrapped tokens can be easily integrated into other Dapps and get listed on exchanges. More Dapps and projects on TomoChain are expected to be integrating and utilising TRC20 wrapped tokens in the future.

Check [TRC20 token integration tutorial](https://docs.tomochain.com/developer-guide/integration/trc20-exchange-wallet-integration).

### **TRC25- Seamless Experience**

TRC25 is an token standard similar to TRC20 plus the ability to let token holders to pay transaction fee using the token itself. Without having store TOMO inside their wallet, user can still transfer the token or delegate it to someone. This will create a better experience for non-web3 user when using the ecosystem.

TRC25 also have an expanded use to enable any smart-contract to have transaction fee sponsor for users of their contract.

### **TRC721- Non-fungible token.**

Non-fungible tokens (NFTs) are all distinct and special. Every token is rare, with unique characteristics, its own metadata and special attributes. Most of the time when people think about NFT, they refer to the successful CryptoKitties game as the standard for crypto-collectibles. However, there are many other applications for TRC721 tokens. Please check our[ other guide](https://medium.com/tomochain/how-to-deploy-nft-tokens-on-tomochain-fe476a68594d) about more use-cases for NFT and the process to deploy an NFT token on TomoChain
