---
description: >-
  Blockchain comparison overview: TomoChain, Ethereum, EOS, Cardano and
  Tendermint.
---

# Blockchain Platform Comparison

## Bitcoin, Ethereum and Blockchain <a id="5994"></a>

Blockchain, the technology behind Bitcoin, has developed over the last decade into one of today’s biggest and most groundbreaking technologies, with the potential to impact every industry from financial to manufacturing, healthcare and educational institutions. Later on, launched in 2015 by Vitalik Buterin, Ethereum is the most notable public blockchain infrastructure after Bitcoin. Ethereum provides a Turing complete language for writing smart contracts. The latter can be automatically executed based on a set of criteria established in the Ethereum blockchain.

Despite the explosive momentum gained, and promises of Bitcoin and Ethereum, there are still intrinsic issues, especially related to transaction processing performance. Both Bitcoin and Ethereum use Proof-of-Work \(PoW\) in their consensus algorithm where an extraordinary amount of computing power is spent for calculations, called mining, in order to create a block. On the other hand, Bitcoin and the current Ethereum provide very poor performance in terms of transaction processing speed: around 10 transactions per second which is incomparable to traditional electronic payment systems such as VISA and MasterCard.

## The shift to the more environmentally friendly, and more efficient Proof-of-Stake <a id="e443"></a>

Proof-of-Stake \(PoS\) aims to provide a more environment-friendly and efficient consensus protocol. With PoS, the creator of a new block “[is chosen in a deterministic way, depending on its wealth, also defined as a stake](https://steemkr.com/blockchain/@sheydboss/a-very-brief-history-of-blockchain-technology-everyone-should-read)”. Some notable proponents of this shift are [EOS](https://eos.io/), [Ethereum Casper FFG](https://arxiv.org/pdf/1710.09437.pdf), [Cardano](https://www.cardano.org/en/home/), [Tendermint](https://tendermint.com/) and [TomoChain](https://tomochain.com/).

> These blockchain solutions are not only trying to provide solutions for the energy and cost savings but also promise to solve the blockchain performance problem as well. While some PoS-related similarity is undoubtedly shared between these blockchains, many differences are yet to be analysed.

In this post, we will show how TomoChain compares with EOS, Ethereum, Cardano and Tendermint. The aspects used for the comparison include _consensus protocol, decentralisation, security, scalability/performance, roadmap, and ecosystem_.

![](../../.gitbook/assets/ba-ng-bie-u-so-sanh-01%20%281%29.png)

## Overview of TomoChain <a id="b088"></a>

The blockchain industry and the infrastructure of the Internet of Value are being built rapidly around the globe, and to many the atmosphere is eerily similar to the building of the Internet in the late ’90s, with pioneers and dreamers coming together to build a new future. The objective of TomoChain is to become a leading part of this phenomenon through seamlessly merging an ecosystem of applications, with cryptographic tokens used by millions of mainstream users and a unique blockchain infrastructure architecture, allowing for fast, frictionless payment and a secure, decentralised, and trusted store of value.

> TomoChain aims to be a public EVM-compatible blockchain with the following advantages: low transaction fees, fast confirmation time, double validation and randomization for security guarantees. TomoChain envisions an ecosystem of different Dapps running on the TomoChain blockchain infrastructure.

In particular, we propose a solution for solving the transaction processing performance bottleneck in Ethereum which hinders its adoption into industries, especially finance. More specifically, we are constructing an efficient and secured consensus protocol, which tackles the following main bottlenecks of classic blockchains:

* _Efficiency: The small throughput of Bitcoin and Ethereum severely hinders a widespread adoption of such crypto- currencies._
* _Confirmation times: Bitcoin takes on average 1 hour to confirm a transaction because the confirmation of a Bitcoin block requires 5 subsequent blocks created following it. While Ethereum uses a smaller block-time, the average confirmation time still remains relatively high, around 13 minutes. These long confirmation times hinder many important applications \(especially smart contract applications\)._
* _Fork generation: The problem of fork chain consumes computational energy, time, and creates potential vulnerabilities for different types of attacks._

[In the technical paper](https://tomochain.com/docs/technical-whitepaper--1.0.pdf), TomoChain proposes the Proof-of-Stake Voting \(PoSV\) consensus, which is a PoS-based blockchain protocol with a fair voting mechanism, rigorous security guarantees, and uniform probability eventually. The consensus has the following key novelties:

* _Double Validation to strengthen security and reduced fork risk_
* _Randomization to guarantee a fair division of labour between Masternodes, and prevent handshaking attacks_
* _Fast confirmation time and efficient checkpoints for finality or rebase_

TomoChain Team is currently implementing these mechanisms based on the Ethereum source code.

## Overview of EOS.IO <a id="c0a8"></a>

[The EOS.IO blockchain architecture is designed to enable vertical and horizontal scaling of decentralised applications](https://github.com/EOSIO/Documentation/blob/master/TechnicalWhitePaper.md). This is achieved by creating an operating system-like construct upon which applications can be built. EOS.IO offers a blockchain architecture that may ultimately scale to millions of transactions per second, eliminate user fees, and allow for quick and easy deployment and maintenance of decentralised applications, in the context of a governed blockchain. EOS.IO, led by Daniel Larimer, relies on the Delegated Proof-of-Stake \(DPoS\) consensus protocol, which stems from the Bitshares DPoS. Its performance promises to scale to millions of transactions per second with a great ecosystem of Dapps running on it.

## Overview of Cardano <a id="cda2"></a>

Cardano is the first full open-source decentralized public blockchain and cryptocurrency project based on peer-reviewed academic work implemented in Haskel. It is developed by IOHK engineering body in conjunction with multiple universities. Cardano uses the a secure Proof of Stake consensus, namely, Ouroboros. The latter is backed by strong researches and sound mathematical formalisations and proofs that provide more confidence about security and scalability. [Cardano promises to allow for developers to build decentralised applications and contracts and run them in a low-cost, secure, private, scalable and legal environment](https://www.cryptomorrow.com/2017/10/10/is-cardano-better-than-ethereum/). On one hand, Cardano Ouroboros is geared towards user privacy. On the other hand, it also takes into consideration the needs of regulators in order to easily upgrade the system. In doing so, Cardano claims being [the first protocol to balance these requirements in a nuanced and effective way, pioneering a new approach for cryptocurrencies.](https://cardanofoundation.org/protocol/#technological-innovation)

## Overview of Tendermint <a id="f783"></a>

[The Tendermint blockchain infrastructure is designed to be easy-to-use, simple-to-understand, highly performant, and useful for a wide variety of distributed applications](https://tendermint.readthedocs.io/projects/tools/en/master/introduction.html). Tendermint aims for secure and consistent replication of an application on many machines. Security means that Tendermint works even if up to 1/3 of machines fail in arbitrary ways. Consistency means that every non-faulty machine sees the same transaction log and computes the same state. These two properties play a critical role in the fault tolerance of a broad range of applications, from currencies, to elections, to infrastructure orchestration, and beyond.

Tendermint consists of a consensus engine, called Tendermint Core and a generic application interface. Tendermint Core relies of the PoS and [Byzatine Fault Tolerance \(BFT\)](https://medium.com/loom-network/understanding-blockchain-fundamentals-part-1-byzantine-fault-tolerance-245f46fe8419) to ensure that every machine stores the same transactions in the same order. On the other hand, the application interface enables the transactions to be processed in any programming language. Therefore, developers can use Tendermint for BFT state machine replication of applications written in whatever programming language and development environment is right for them.

## Comparison criteria <a id="4c41"></a>

## Consensus <a id="2ab4"></a>

Consensus is undoubtedly the core mechanism of any decentralized cryptocurrency. It maintains the consistency, immutability, and security of the blockchain on all full nodes of decentralized systems. Bitcoin blockchain with its Proof-of-Work provides securities and decentralization but leaving its scalability as bottleneck. Since then, many consensus protocols have been proposed to leverage. These mechanisms include many variants of Proof-of-Stake-based consensus protocols that are found in the aforementioned projects. The latter do not only aim for solving the energy wasting problem of current Bitcoin and Ethereum but also for improving transaction processing performance.

## Decentralization <a id="4da0"></a>

One of the facts that make the Bitcoin blockchain become a subject of great interest lies in its decentralization. Different from existing centralized systems and/or what we call “closed distributed systems”, Bitcoin operates on an “_open_” or “_permissionless_” decentralized systems where any node can join and leave the network, and makes the joining-leaving of nodes become “_daily activities_” that it must deal with. By this way, the single points of failure problem residing in centralized systems can be eliminated. As a result, the more decentralization a system offers, the more data availability and fault tolerance it supports.

## Security <a id="bbcc"></a>

One of the clearly visible and pioneering applications of blockchain is in financial industry. The current total market cap of cryptocurrencies is more than 300 billions of dollars, which incentivizes attackers to penetrate or attack the system. There are many attack types to these systems such as double-spending, nothing-at-stake, spamming, DDoS and long range attacks. Blockchain-based cryptocurrency systems must not only deal with these attacks but also ensure the stability of the system, which includes safety and liveness.

## Scalability/performance <a id="55b8"></a>

Current financial technologies such as Visa and Master can handle thousands of transactions per second, which definitely defeat the poor transaction processing performance of Bitcoin and Ethereum. Thus, in order for the latter to gain more adoption to the financial industry as well as other industries such as logistics and manufacturing, blockchain technologies must leverage its scalability/performance. Therefore, we consider performance as one of the key criteria to evaluate the success of a blockchain system.

## Roadmap <a id="1d77"></a>

Generally speaking, a technology roadmap is a flexible planning technique to support strategic and long-range planning, by matching short-term and long-term goals with specific technology solutions. Roadmap is one of the important aspects for assessing the potential as well as the vision of a project.

## Ecosystem <a id="08c1"></a>

All the aforementioned blockchain projects are building infrastructure upon which other Dapps can be built. The stronger the infrastructure and its support, the more Dapps can be based on it for creating a strong ecosystem. Moreover, a strong ecosystem of Dapps will attract more users of the infrastructure, which in turn motivates improvements and entails the development of the underlying infrastructure. Each of the above blockchain projects provides PoS-based consensus that can handle thousands of transactions per second, thus promises many potentials Dapps for the ecosystem.

