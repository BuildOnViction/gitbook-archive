---
description: Glossary of blockchain and crypto terms
---

# Glossary

### Generals

| Term | Description |
| :--- | :--- |
| Blockchain Network | A blockchain network is a computer network that consists of nodes. |
| Block time | The duration between 2 consecutive blocks |
| Epoch | Each epoch consists of 900 blocks. |
| Masternode | Masternodes are full-nodes that create, verify and validate new blocks in TomoChain’s platform. |
| TOMO | TOMO is the native currency of the TomoChain ecosystem. |
| Relayer | A relayer is a decentralized exchange run on top of TomoX. |
| Consensus | The algorithm that allows many masternode nodes to reach an agreement. In case of blockchain, the agreement is on creating blocks. |
| PoSV | Proof-of-Stake Voting is the TomoChain consensus protocol that helps all nodes in TomoChain's network to reach agreement about the blockchain. |

### TomoX

<table>
  <thead>
    <tr>
      <th style="text-align:left">Term</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Relayer</td>
      <td style="text-align:left">A DEX interacts with TomoX protocol. A relayer collects all trading orders
        of that relayer and sends them all to the masternode network, which then
        process the orders following the TomoX protocol.</td>
    </tr>
    <tr>
      <td style="text-align:left">TomoX</td>
      <td style="text-align:left">The decentralized exchange protocol built in the core layer of TomoChain
        that allows all relayers to interact with to process trading orders.</td>
    </tr>
    <tr>
      <td style="text-align:left">TomoX-SDK</td>
      <td style="text-align:left">A tool suite that allows to create a TomoX relayer within a few minutes</td>
    </tr>
    <tr>
      <td style="text-align:left">Relayer owner</td>
      <td style="text-align:left">The owner of the wallet address that makes the deposit of 50k TOMO into
        TomoX to propose a new relayer.</td>
    </tr>
    <tr>
      <td style="text-align:left">Relayer deposit amount</td>
      <td style="text-align:left">50k TOMO deposited by the relayer owner to propose a new relayer.</td>
    </tr>
    <tr>
      <td style="text-align:left">Trader trading fee</td>
      <td style="text-align:left">Fee that traders must pay Relayer and is 0.1% of trading amount. Trader
        Trading fee is set/adjusted by Relayer Owner on the smart contract. Trader
        Trading fee is paid in Base Token when the corresponding order is matched.
        Trader Trading fee is sent to Relayer Owner Address.</td>
    </tr>
    <tr>
      <td style="text-align:left">Relayer Trading Fees</td>
      <td style="text-align:left">
        <p>Taker&#x2019;s Relayer has to pay a flat trading fee of 0.001 TOMO for
          the masternode that includes that trade in a block.</p>
        <p>Maker&#x2019;s Relayer has to pay a flat trading fee of 0.001 TOMO for
          the masternode that includes that trade in a block.</p>
        <p>Relayer&#x2019;s trading fee is charged when the order is matched. Relayer
          Trading fee is then sent directly to the Masternode Owner Address.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Maker</td>
      <td style="text-align:left">Trader who creates an order that does not match any order in the order
        book</td>
    </tr>
    <tr>
      <td style="text-align:left">Taker</td>
      <td style="text-align:left">Trader who creates orders that immediately match other orders in the order
        book</td>
    </tr>
  </tbody>
</table>

### TomoP

| Term | Description |
| :--- | :--- |
| Privacy Address | The address that is used for receiving TOMO/tokens privately on TomoChain. Even though the recipient's privacy address is needed in making private transactions, the privacy address is never publicly appeared on the TomoChain blockchain, thus no one would be able to trace who's the recipient in the transaction. |
| Privacy contract | The smart contracts that are used for anonymizing TOMO and tokens to make private transactions. All private transactions will have the privacy contract as the destination. |
| Dual-key address | Each privacy account/wallet has a private spend key and private view key for making privacy transactions. A private view key is used for viewing an encrypted private transaction while a private spend key allows to actually `spend` the funds of the privacy account. |
| Sender anonymization | TomoP allows to anonymize transaction senders, thus no third-party would be able to know transaction senders without permission of the transaction senders \(by giving the third-party the corresponding private view key\) |
| Receiver Anony | TomoP allows to anonymize transaction receivers by using stealth addresses |
| Stealth address | A stealth address is a one-time generated public key that is generated using a cryptographic scheme based on the the transaction recipient privacy address. Basically, a stealth address of is a public key generated by the `transaction sender` but the corresponding private key can only be deduced from the private view and spend keys of the corresponding recipient. |
| TomoP transaction fee | The current fee for sending TOMO privately is 0.01 per private transaction.  |
| TomoZ integration | TomoP relies on TomoZ in anonymizing transaction senders. The idea is that TomoP transaction gas fees will be paid from a fee vault deposited in TomoIssuer, while actually fees will be paid in the smart contract itself. |
| TRC21P token | A standard token that is built based on TomoP. The token standard allows all transactions to be private. |

