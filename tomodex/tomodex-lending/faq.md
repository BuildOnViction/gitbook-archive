# FAQ

### What is P2P lending?

P2P lending is a service to help match lenders with borrowers without the participation of financial intermediaries. Collateralized assets are stored safely in smart contracts secured by the TomoX protocol. TomoDEX \(lending\) allows users to set their own interest rates and terms.

### What coins/tokens are accepted as collateral?

You can deposit the following crypto assets: BTC, ETH, TOMO as collateral via [TomoBridge](https://bridge.tomochain.com). Support for other major altcoins are coming later.

### How much collateral is needed for creating a loan?

Collateral Deposit Rate: 150% of the total loan value. 

For example: If a user wants to borrow 1000 USDT against BTC and the BTC price is 7,500 USDT, the user must deposit = 1,000 \* 150% / 7,500 = 0.2 BTC 

### How much interest will I pay?

In addition to repaying the principal, or original amount borrowed, the Borrower has to pay interest to the Lender. The interest is calculated as follows:

$$
I = F * R * \frac{T}{365}
$$

* I: Interest
* F: The original amount borrowed
* T: Term \(days\) \(e.g. 1 days, 14 days, 30 days …\)
* R: Annual interest rate 

### What happens if I don’t repay my loan?

The Borrower has to repay the value of the loan and the interest of the loan to the Lender before the due date. By default, if the Borrower has enough balance of the borrowed asset, TomoX will automatically repay the loan on the due date. ****

### **Can I repay my loan early?**

You can make loan repayments at any time ****but ****no partial repayment is allowed.   
If the Borrower decides to pay off the loan early, aside from the normal interest he has to pay until that point, he will be charged a prepayment penalty \(which is equal to half of the interest he would have had to pay from that point till the maturity date\).

$$
I = F * R * \frac{T_1 + T}{2*365}
$$

* I: Interest
* F: The original loan amount
* T: Term \(days\) \(1 days, 30 days …\)
* T1: The number of days borrowed.
* R: Annual Interest rate

### How do auto liquidations due to price volatility work for loans?

Liquidation Rate: 110% of the total loan amount . 

This means that the collateral will be automatically liquidated and released to the Lender’s Address if its market value falls to 110 % of the loan value.

Market value of a collateral = Market price of the collateralized asset \* Quantity of the collateralized asset

{% page-ref page="../../masternode-and-dex/tomox/tomox-p2p-lending.md" %}



