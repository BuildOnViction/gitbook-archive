# TomoX P2P Trading

## Trading Fees

Trading fees are categorized as trader fees and relayer fees:

**Trader fees:** Fees that traders must pay the Relayer. These fees will be automatically deducted from the User's wallet when successfully matched.

**Relayer fees:** Fees that relayers must pay the Masternode network. These fees will be automatically deducted from the Trading Fee Fund when successfully matched.  


### Trader Trading Fees

* Seller Fee: 0.1 %
* Buyer Fee: 0.1% 
* Trader Trading fee is set/adjusted by the Relayer Owner on the smart contract. 
* Trader Trading fee is charged by the Quote Token at the time that the order is matched. 

Trader Trading fee is sent to the Relayers’ Owner Address.  


**E.g: Pair TOMO/USDT**

* TOMO -&gt; Base Token
* USDT -&gt; Quote Token

=&gt; The trading fee will be charged by USDT.  


### **Relayer Trading Fees**

* The Seller’s Relayer pays a flat trading fee of 0.001 TOMO to the Masternode that creates the block which contains the trade.
* The Buyer’s Relayer pays a flat trading fee of 0.001 TOMO to the Masternode that creates the block which contains the trade.
* The Relayer’s trading fee is charged at the time that the order is matched.
* The Relayer’s trading fee is sent to the Masternode Owner Address that created the block.  

## **Cancellation Fees**

### Trader Cancellation Fees

* The Trader’s Cancellation fee is equal to 1/10 \(cancellation fee: 0.01%\) of the Trader’s trading fee in the Base Token if as a seller and in the Quote Token if as a buyer.
* The Trader’s Cancellation fee is charged at the time that the trader cancels the order.
* The Trader’s Cancellation fee is sent to the Relayers’ Owner Address

### **Relayer Cancellation Fees**

* Relayer has to pay a Relayer’s Cancellation fee of 0.0001 TOMO for Masternode that creates the block containing the cancel order.
* Relayer’s Cancellation fee will be charged at the time that the trader cancels the order. Relayer’s Cancellation Fee is sent to the Masternode Owner Address that created the block.

{% hint style="info" %}
Relayer fees: Fees that relayers must pay the Masternode network. These fees will be automatically deducted from the \*Trading Fee Fund when successfully matched. 

The 25,000 TOMO deposit of the Relayer Owner will be divided into 2 parts:

* Locked Funds: 20,000 TOMO will be locked and only be available for withdrawal 30 days after the relayer owner makes a decision to resign. 
* Trading Fee Fund: 5,000 TOMO will be used for paying network fees, and be deducted from as fees are sent to masternodes for handling trades and order processing
{% endhint %}





  


  
  


