---
description: >-
  This article will guide how to deploy a TRC-21 token on TomoChain
  step-by-step.
---

# How to Deploy a TRC21 Token on TomoChain

The [TomoZ](http://bit.ly/TomoZWhitePaper) protocol aims to solve a critical user adoption issue found in nearly every major smart contract platform. TRC21, empowered by TomoZ, allows token holders to pay transaction fees by the token itself without holding any TOMO in their wallet. [TomoIssuer](https://issuer.testnet.tomochain.com/) is the final piece of the big picture. TomoIssuer provides a user-friendly interface for any token issuer to issue a TRC21 token _without any coding experience required_. This article will guide how to deploy a TRC-21 token on TomoChain step-by-step.

Below are the most important features of TomoIssuer that have made it a revolutionary tool:

* **User-Friendly Interface**: Issue a TRC21 token in only a few steps.
* **No Coding Experience Required**: No prerequisite knowledge about smart contract programming is needed.
* **Token Customization Options**: Customize the token supply, token name, and minimum transaction fee through TomoIssuer’s dashboard.

**Let’s Start the Tutorial!**

On the homepage there are two main options with the TomoIssuer. The first one is to create a new TRC21 token and the second one is to donate a fee for an existing TRC21 token.

**Step 1:** Go to Token Issuance dashboard, then set the parameters. From top to bottom: Token’s Name; Token’s Symbol; Token’s Total Supply, and Token’s Decimal. A small issuance fee will be charged, make sure that the used wallet has enough TOMO.

* The `symbol` of the token contract is the symbol by which the token contract should be known, for example “MYT”. It is broadly equivalent to a stock ticker, and although it has no restriction on its size it is usually 3 or 4 characters in length.
* `decimals` refers to how divisible a token can be, from 0 \(not at all divisible\) to 18 \(pretty much continuous\) and even higher if required. Technically speaking, the `decimals` value is the number of digits that come after the decimal place when displaying token values on-screen.¹

![](../../.gitbook/assets/image%20%2835%29.png)

**Disclaimer:** The token issuance fee is not fixed. The exact number will be announced when TomoIssuer mainnet launch.

**Step 2:** TomoIssuer will ask for the token’s information to confirm. Please check all the criteria carefully before clicking on the “Issue token” and wait for the contract to be deployed.

![](../../.gitbook/assets/image%20%2827%29.png)

**Note:** Any developer with some experience of developing and deploying smart contracts can refer to our reference implementation of the [TRC21 standard](https://docs.tomochain.com/wp-and-research/specs/trc21_standard/) to make customizations to the deployed token contract.

![](../../.gitbook/assets/image%20%2825%29.png)

**Step 3:** A notification is received when the token is successfully issued. Click “View detail” to check the token’s summary including: number of holders, transactions, etc. Choose “Apply to pay fee by any token” for TomoZ integration.

![](../../.gitbook/assets/image%20%2823%29.png)

**Step 4:** Once deployed, the issuer needs to agree that the fees for all transactions to the newly deployed token contract will be paid in terms of the issued token. Once the conditions are agreed to move to the next step by clicking “I understand”

![](../../.gitbook/assets/image%20%2815%29.png)

**Step 5:** The token issuer needs to deposit a minimum amount of 10 TOMO. The deposit can’t be withdrawn. TOMO held in the deposit pool is deducted to pay the Masternodes for transaction processing.

![](../../.gitbook/assets/image%20%2844%29.png)

**Step 6:** Congratulations! Now the new TRC21 token can be used. Edit the transaction fee in the token itself. Change this number at any time during the operation of the token.

![](../../.gitbook/assets/image%20%2846%29.png)

**Step 7:** In the token management dashboard, there are buttons to interact with the tokens, such as transfer and deposit more TOMO to pay for subsequent transaction fees. Don’t forget to check the TRC21 fee fund because transactions will not be processed if the remaining deposit is not enough to pay transaction fees.

![](../../.gitbook/assets/image%20%2853%29.png)

**Donate TOMO for TRC21 transaction fees**

If the TOMO funds of the token issuer in TomoIssuer are not enough to pay for subsequent transaction fees, any token holders can deposit more TOMO to the TomoIssuer contract to continue making transactions.

Go to donate transaction fee tab from TomoIssuer’s homepage. Enter the name of the appropriate token to donate TOMO to, then input the donation amount. Considering that the transaction fee in TomoChain is near-zero, 1 TOMO can power thousands of transactions.

![](../../.gitbook/assets/image%20%2848%29.png)

Transfer the TRC21 token to anyone just by going to “transfer token”. TomoWallet \(testnet version\) will start running in a new tab so issued tokens can be transferred easily.

![](../../.gitbook/assets/image%20%2859%29.png)

The details of TRC21 token transactions are displayed on TomoScan. TomoScan will show transaction fees in terms of the token and actual fee in TOMO like a normal transaction.

![](../../.gitbook/assets/image%20%2814%29.png)

**Congratulations!** You have learned about how to deploy a TRC21 token on [TomoChain](http://tomochain.com/).

\(1\) [Understanding ERC-20 token contracts](https://medium.com/@jgm.orinoco/understanding-erc-20-token-contracts-a809a7310aa5)

\(2\) [Video tutorial](https://www.youtube.com/watch?v=lGWVkhNpmSQ&feature=emb_title) for your preference

