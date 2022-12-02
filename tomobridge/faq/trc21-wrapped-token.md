# TomoChain Wrapped Tokens

**1. What are TomoChain Wrapped Tokens?**

TomoChain Wrapped Tokens are tokens hosted on the TomoChain public blockchain, issued by TomoBridge Pte. Ltd. and backed by an equivalent amount of the underlying assets or currencies from a different blockchain.&#x20;

There are two types of TomoChain wrapped tokens including **TRC20 wrapped token** and **TRC21 wrapped token**.&#x20;

### **2. Why do I need TomoChain Wrapped Tokens?**

TomoChain wrapped tokens can bring more liquidity from other blockchain networks, and allow the token holders to benefit from the fast transactions and low fees of the TomoChain blockchain. TomoChain wrapped tokens can be transferred, traded, integrated into other dapps just like the native tokens on TomoChain.\
****

## **3. What are the differences between TRC20 and TRC21 wrapped tokens?**

Essentially, these two types of wrapped tokens are TRC20 and TRC21 standard tokens respectively. Check below for the differences between TRC20 and TRC21 tokens.

**TRC20:** TRC20 is an equivalent token standard of ERC20 built on top of the TomoChain blockchain. TRC20 token holders would need to hold a small amount of TOMO to cover the extremely low transaction fees.&#x20;

TRC20 wrapped tokens can be easily integrated into other Dapps and get listed on exchanges. More Dapps and projects on TomoChain are expected to integrate and utilize TRC20 wrapped tokens in the future.

TRC20 wrapped tokens can be traded on LuaSwap (TomoChain version). \
****

**TRC21:** TRC21, powered by TomoZ Protocol, creates a frictionless experience for non-crypto users by allowing token holders to pay transaction fees by the token itself without having to hold any TOMO in their wallet.&#x20;

TRC21 wrapped tokens can be traded on LuaSwap (TomoChain version) and all TomoX’s DEXs including TomoDEX (Though listing depends on each DEX's decision).\


&#x20;** **_**TRC20 wrapped token vs TRC21 wrapped token**_&#x20;

| _****_               | **TRC20 Wrapped Token** | **TRC21 Wrapped Token**  |
| -------------------- | ----------------------- | ------------------------ |
| **Trade on TomoDEX** | **×**                   | **√**                    |
| **Trade on LuaSwap** | **√**                   | **√**                    |
| **Transaction Fee**  | **In TOMO**             | **In Transaction Token** |

### **4 . What does it mean by "Wrap/Deposit" and "Unwrap/Withdraw"?**

Due to the different blockchain networks, users can only swap their TomoChain wrapped tokens to/from the other blockchain tokens via a designated bridging portal.

Swapping other blockchain tokens to TomoChain wrapped tokens is known as "**Wrap**" or “**Deposit**”. Swapping from TomoChain wrapped tokens to other blockchain tokens is known as “**Unwrap**” or “**Withdraw**”

{% hint style="info" %}
The meaning of “Deposit” here is different from traditional centralized exchanges. On TomoDEX, users are always in direct custody of their funds. Which means you trade directly with the funds in your wallet without having to put it into the exchange’s account.
{% endhint %}

### **5. How can I wrap and unwrap my token?**

You can go to[ TomoBridge](http://bridge.tomochain.com/) to swap between the native token and a TomoChain wrapped token. Check out this article for details: [_**TomoBridge Tutorial**_](../tutorial/#fda7)_****_

### **6. Can I send my TomoChain wrapped token directly to an ERC20 address, or vice versa?**

In simple words, NO you shouldn’t.

### **7. What should I do if I mistakenly sent a TomoChain wrapped token to an ERC20 address without unwrapping, or vice versa?**

There are a few different scenarios including but not limited to the following:

**a.) If the receiving address is your own wallet address**

The TomoChain and Ethereum networks share the same wallet address, which means if you have access to the address of one network, you can access the same address of the another. All you have to do is to switch the network on your wallet.

Let’s say you sent a TRC21 token to an ERC20 address, then you can retrieve your funds by following the steps below (similar process the other way around):

1. Log into your ERC20 wallet
2. Add the TomoChain network to your wallet (follow [this guide](https://docs.tomochain.com/general/how-to-connect-to-tomochain-network))
3. Switch to the TomoChain network to retrieve your funds

If the wallet you use doesn’t support multiple networks, below is an alternative solution:&#x20;

1. Log into your ERC20 wallet and export the Private Key. (It has to be the Private Key, not Mnemonics)
2. Log into your [TomoWallet](https://wallet.tomochain.com/#/my-wallet) with the Private Key to retrieve your funds. (Instead of using TomoWallet, you can also choose to log into TomoDEX or TomoBridge so you can unwrap directly from there)

{% hint style="info" %}
Some wallets may not come with a Private Key when you created your address, like Trust Wallet. Then you might need to contact the wallet developer to help you export your Private Key.
{% endhint %}

For Trust Wallet users, please follow[ this guide](https://community.trustwallet.com/t/how-to-recover-funds-sent-to-a-wrong-public-address/145) to export your Private Key:

**b.) If the receiving address belongs to a third party (ex. an exchange)**

In this case, the third party team is now holding your funds. You have to contact them directly for the funds recovery.

Most exchanges would provide this service for a fee. But each company is different and it depends on their own policy.

**c.) If the receiving address belongs to TomoBridge**

[Follow this guide](https://medium.com/tomochain/tomobridge-funds-recovery-support-and-terms-efe9092a1427) to submit a support ticket. \
