# FAQ

### 1. What is TomoBridge?

TomoBridge is the cross-chain transfer module for interoperability between TomoChain and other crypto assets chains

### 2. What is TRC21  WrappedToken?

A Wrapped Token is a TRC21 token hosted on the TomoChain public blockchain, issued by TomoBridge Pte. Ltd.  and  backed by an equal amount of the underlying asset or currency. TRC21 Wrapped BTC, for instance, is a token worth the same as one BTC at any given moment. More details about [TRC21 Wrapped Tokens](trc21-wrapped-token-information.md).

TRC21 tokens are issued on TomoZ Protocol to bring users a much more friendly trading experience with a blazing fast speed, and extremely low gas fees that can be paid by the transaction token itself. It will also be supported by TomoP Protocol to enable a bunch of privacy features.

By nature, we can divide TRC21 Tokens into 2 types:  
**Native TRC21 Token**: The tokens that are originally issued on TomoChain blockchain, like TOMO, AIS, TIIM, and etc.  
**TRC21 Wrapped Token**: The tokens that are issued on other blockchains originally, and then reproduced on TomoChain network by locking a same amount of the native asset into a smart contract or multi-signiture wallet, like BTC, ETH, USDT, YFI, and etc.

### 3. Why do I need TRC21 Wrapped Tokens?

The reason you need TRC21 Wrapped Token is to be able to trade other platform's native token like BTC or ETH on decentralized exchange like TomoDEX. Because decentralized platforms running on TomoX use smart contracts to execute trades directly between traders and they need to have the same token standard.

{% hint style="info" %}
All the tokens listed on TomoDEX are TRC21 Tokens.
{% endhint %}

### 4. Can I trade TRC21 Wrapped Tokens on TomoX's DEXs after swapping?

Yes, you can use TRC21 Wrapped Tokens on [TomoDEX](https://dex.tomochain.com) as well as other DEXs built on top of TomoX.

### 5. Which coin is supported by TomoBridge?

TomoBridge currently supports converting between BTC, ETH, USDT, FTT, YFI, SRM, DEC, DXD, VNDC and their corresponding TRC21 tokens. 

###  6. What does it mean by "Wrap/Deposit" and "Unwrap/Withdraw"?

Due to the different token standards, you can only swap your TRC21 Wrapped Token to/from the other blockchain tokens via designated bridging portals.

Swapping other blockchain tokens to TomoChain’s TRC21 Wrapped Tokens is known as to "**Wrap"** or “**Deposit**”.  
Swapping from TomoChain’s TRC21 Wrapped Tokens to other blockchain tokens is known as to “**Unwrap**” or “**Withdraw**”

{% hint style="info" %}
The meaning of “Deposit” here is different from traditional centralized exchanges.  
On TomoDEX, users are always in direct custody of their funds. Which means you trade directly with the funds in your wallet without having to put it into the exchange’s account.  
{% endhint %}

### 7. How can I swap my asset to TRC21 Wrapped Token and vice versa?

You can go to [**TomoBridge**](http://bridge.tomochain.com) and swap between your asset and TRC21 Wrapped Token. Check out this article for details: [_**TomoBridge Tutorial**_](tutorial.md#fda7)_\*\*\*\*_

### **8**_**.**_ Can I sent my TRC21 token directly to an ERC20 address, or vice versa?

**In simple words, NO you shouldn’t.**

TRC21 \(by TomoChain\) and ERC20 \(by Ethereum\) share almost the same address structure. The Private Key that you have for either address can be used to access the same wallet address on the other network.

In other words, the address for TRC21 and ERC20 tokens is the same, with which you can selectively access either asset depending on the network that you are on.

That also means the transaction can be sent through when you transfer your TRC21 Token to an ERC20 address, and the same vice versa, with the token standard remaining unchanged.

**So yes, the transaction can be signed and sent through. But this is probably NOT what you want to do if you look to swap your TRC21 Wrapped Token to/from the native tokens from other blockchains.**

### **9**. What should I do if I mistakenly sent my TRC21 Token to an ERC20 address without wrapping/unwrapping, or vice versa?

There could be a few different scenarios: a.\) If the receiving address is your own wallet address

As explained in Q4, these two token standards share the same address and all you have to do is to switch the network.

Let’s say you send your TRC21 Token to an ERC20 address, then you can retrieve your funds by following the steps below \(similar process the other way around\):

1. Log into your ERC20 wallet and export the Private Key. \(It has to be the Private Key, not Mnemonics\)
2. Log into your TomoWallet with the Private Key to recover your fund. \(Instead of TomoWallet, you can also choose to log into TomoDEX or TomoBridge so you can unwrap directly from there\)

{% hint style="info" %}
Some wallets may not come with a Private Key when you created your address, like Trust Wallet. Then you might need to contact the wallet developer to help you export your Private Key.
{% endhint %}

For Trust Wallet users, please follow this guide to export your Private Key: [https://community.trustwallet.com/t/how-to-recover-funds-sent-to-a-wrong-public-address/145](https://community.trustwallet.com/t/how-to-recover-funds-sent-to-a-wrong-public-address/145) b.\) If the receiving address belongs to a third party \(ex. an exchange\)

In this case, the third party team now is holding your funds. You will have to contact them directly to help you look into their account and refund it for you.

Most exchanges are willing to do it for their users for a fee. But each company could be different and it depends on their own policy.

### **10. What can I do when having issues on** TomoBridge?

Please [submit a request](https://forms.gle/LgEGzd35Vg8SEpGQ6) to report your issue with the TomoBridge support team of contact with us on Telegram channel at [https://t.me/TomoDEX\_Official](https://t.me/TomoDEX_Official)

### TOMOB

[**TOMOB**](https://medium.com/tomochain/tomob-is-officially-listed-on-binance-dex-4dd83117e515) **is a prime use case for TomoBridge. TomoChain has issued BEP-2 TOMO tokens on Binance Chain called TOMOB.**

#### 1. Is TomoChain migrating to Binance Chain?

No, we are not. We are simply offering a 2-way bridge to allow TomoChain holders to operate on Binance Chain \(TomoChain &lt;-&gt; Binance Chain\). This is TomoChain’s first real test of cross-chain compatibility using TomoBridge.

#### 2. What is TOMOB?

TomoChain has issued BEP-2 TOMO tokens on Binance Chain called TOMOB. With the creation of TOMOB, we have locked up an equal number of native TOMO to ensure the total supply remains the same.

#### 3. Can I trade TOMOB on Binance DEX now after swapping? <a id="can-i-trade-tomob-on-binance-dex-now-after-swapping"></a>

Yes, you can.

#### 4. How do I swap my TOMO to TOMOB and vice versa? <a id="how-do-i-swap-my-tomo-to-tomob-and-vice-versa"></a>

Go to [TomoBridge for TOMOB](htttps://tomob.tomochain.com) and swap between TOMO and TOMOB. Check out this video for details: [How to swap between TOMO and TOMOB?](https://www.youtube.com/watch?v=TglV_VyAYI4&feature=youtu.be)

#### 5. Can TomoB be staked? <a id="can-tomob-be-staked"></a>

No, you can't stake TomoB.

