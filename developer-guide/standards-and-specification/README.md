---
description: >-
  In this guide, we take a look at different token standards on the TomoChain
  platform.
---

# Standards & Specification

## **Overview**

In every blockchain ecosystem the token functions as the central element of a new type of economy. A token standard defines a set of rules that governs its issuance and use.

You may be familiar with ERC (Ethereum Request for Comments), which is a technical standard used for smart contracts on the Ethereum. This terminology is the origin of TRC tokens - the equivalent of ERC on TomoChain.

### **Fungible and Non-fungible token**

There are two token standards on TomoChain so far: TRC25 and TRC725. These token standards can be divided into two different categories: fungible and non-fungible tokens. Fungible tokens are all equal and divisible, non-fungible tokens (NFTs) are all distinct and non-divisible.

Fungible tokens are interchangeable and can be divided into smaller token units like TOMO. The fungible token standard TRC25 as digital assets used to offer access to products and/or services on a platform. Non-fungible tokens of the type TRC725 are those that represent a unique asset, like a certificate or a collectible in-game item. The table below compares the differences between three types of token standards on TomoChain.

|                                                 | **TRC25**                | **TRC725**        |
| ----------------------------------------------- | ------------------------ | ----------------- |
| **Divisibility**                                | **Divisible**            | **Non-Divisible** |
| **Technical requirements for Dapp integration** | **Moderate**             | **Moderate**      |
| **Technical requirements for exchange listing** | **Moderate**             | **N/A**           |
| **Transaction Fee**                             | **In Transaction Token** | **In TOMO**       |

### **TRC25 - Gas-less transaction experience**

TRC25 is an token standard similar to ERC20 plus the ability to let token holders to pay transaction fee using the token itself. Without having store TOMO inside their wallet, user can still transfer the token or delegate it to someone. This will create a better experience for non-web3 user when using the ecosystem.

TRC25 also have an expanded use to enable any smart-contract to have transaction fee sponsor for users of their contract.

### **TRC725- Non-fungible token**

Non-fungible tokens (NFTs) are all distinct and special. Every token is rare, with unique characteristics, its own metadata and special attributes. Most of the time when people think about NFT, they refer to the successful CryptoKitties game as the standard for crypto-collectibles. However, there are many other applications for TRC725 tokens.

{% content-ref url="trc25-specification.md" %}
[trc25-specification.md](trc25-specification.md)
{% endcontent-ref %}

{% content-ref url="trc725-specification.md" %}
[trc725-specification.md](trc725-specification.md)
{% endcontent-ref %}
