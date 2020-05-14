# TomoX P2P Lending Fees

### 1. **Service  Fees**

There are 2 types of service fees for using the lending service:

* User service fees: Fees that users pay Relayers. These fees will be automatically deducted from the loan when a match is successful.
* Relayer service fees: Fees that Relayers pay Masternodes. These fees will be automatically deducted from the Trading Fee Fund when a match is successful.

**1.1. User Service Fees**

* Lender service fee: None
* Borrower service fee: 0.5% \(By default\) of the total loan amount payable in the base token\* 

Base token\*: The borrowed asset   


For example: If a user wants to borrow 1000 USDT, he will be charged a service fee of 0.5% \* 1000 = 5 USDT by the Relayer.  


* Lender service fee is non-adjustable
* Borrower service fee rate is set/adjusted by the Relayer Owner.
* Borrower service fee is charged at the time the order is matched.
* Borrower service fee is sent to the Relayer Owner’s Address.

**1.2 Relayer service fees**: Fees that Relayers pay Masternodes. These fees will be automatically deducted from the \*Trading Fee Fund when a match is successful. Relayer has to pay a flat service fee of 0.01 TOMO to the Masternode that creates the block containing the matched order.

* Relayer service fee is charged at the time the order is matched.
* Relayer service fee is sent to the Masternode Owner’s Address.

### 2. Cancellation Fees

There are 2 types of cancellation fees for canceling an order:

* User cancellation fees: Fees that users pay Relayers. These fees will be automatically deducted from the User's wallet.
* Relayer cancellation fees: Fees that Relayers pay Masternodes. These fees will be automatically deducted from the Trading Fee Fund.

**2.1. User Cancellation Fees**

* Lender cancellation fee: The Lender cancellation fee is equal to 1/10 of the Borrower service fee, payable in the Base Token. 
* Borrower cancellation fee:  The Borrower cancellation fee is equal to 1/10 of the Borrower service fee, payable in the collateralized asset.
* Cancellation fee is charged at the time that the Lender/Borrower cancels the order.
* Cancellation fee is sent to the Relayer Owner’s Address

**2.2 Relayer cancellation fees**: Fees that Relayers pay Masternodes. These fees will be automatically deducted from the Trading Fee Fund. 

The Relayer has to pay a flat cancellation fee of 0.0001 TOMO to the Masternode that creates the block containing the canceled order.

* Relayer cancellation fee is charged at the time that the Lender/Borrower cancels the order.
* Relayer cancellation fee is sent to the Masternode Owner’s Address

### 3. Collateral

* Collateral Deposit Rate: 150% \(By default\) of the total loan value. 

For example: If a user wants to borrow 1000 USDT against BTC and the BTC price is 7500 USDT, he has to deposit = 1000 \* 150% / 7500 = 0.2 BTC 

* Collateral Deposit Rate is set/adjusted by the Moderator.
* Collateral will be locked in a non-private key address \(E.g., 0x11\).
* Collateral will be locked at the time the order is matched.
* Collateral will be released at the time the loan is liquidated or closed.
* The collateral for the loan will be released to the Lender’s Address if the loan is liquidated.
* The collateral for the loan will be released to Borrower’s Address if the loan is closed.
* Collateral Price will be equal to the TomoX average price of all the trades \(price \* amount\) in the previous epoch \(called market price\) by the following formula:

$$
\frac{P_1 * V_1 + P_2 * V_2 + .. + P_n * V_n}{V_1 + V_2 + .. + V_n}
$$

* P: Price
* V: Volume
* Pn,Vn: Price and Volume of trade \#n

### 4. Liquidation

Liquidation Rate: 110% \(By default\)

This means that the collateral will be automatically liquidated and released to the Lender’s Address if its market price of the collateralized asset falls to be below the liquidation price.

Liquidation Price = MCP \* LR/DR

* LR : Liquidation Rate
* DR: Collateral Deposit Rate
* MCP: Market price of the collateralized asset at the time the trade is created.

The Liquidation Rate is set/adjusted by the Moderator.

### 5. Order

#### 5.1. Create

#### **5.1.1. Input:**

* Base token \(e.g. USDT\): The asset that the Borrower wants to borrow or the asset that the Lender wants to lend
* Term \(days\) \(e.g. 7, 14, 30 days\): The period over which the Borrower wants to borrow or the period over which the Lender wants to lend
* Collateral \(e.g BTC\): The asset that the Borrower will deposit as a security for the loan or the asset that the Lender accepts as security for extending the loan
* Interest Rate \(annually, e.g. 10%\): The amount above the principle that the Lender charges the Borrower or the amount above the principal that the Borrower is willing to pay the Lender for the loan. The interest rate is set by the Lender/Borrower at the time the LEND/BORROW order is created.
* Side: \(LEND/BORROW\)
* Amount: The quantity of the base asset that the Borrower wants to borrow or the quantity of the base asset that the Lender wants to lend.
* Signature

#### **5.1.2. Status**:

* All orders: Displays all orders - open, filled, canceled, and rejected
* Open orders: All unmatched orders
* Filled orders: All fully matched orders
* Partially filled orders: Any matched order that is only partially filled
* Rejected orders: Any order that is underfunded and cannot pay trading fees or if the balance is under the value of the order
* Canceled orders: All Open/Partially Filled orders that have been manually canceled

#### 5.3. Orderbook

An order book is an aggregate list of the number of LEND and BORROW orders that have been placed at a particular term for a base token.  


#### 5.4. Matching

* If an open LEND order has the same interest rate and the same term with an open BORROW order, the two will be matched together to create a trade. 
* The status of each order will be updated from “Open” to “Filled” or “Partially Filled”. A partial fill is a loan execution where some but not all of an order is filled at the desired interest rate. 
* When matched,
* The collateral for the BORROW order will be locked in a 0x11 address.
* The matched amount of the base token in the Lender’s address will be transferred to the Borrower’s Address.

### 6. Interest

In addition to repaying the principal, or original amount borrowed, the Borrower has to pay interest to the Lender.

The interest is calculated as follows:

$$
I = F * R * \frac{T}{365}
$$

* I: Interest
* F: The original amount borrowed
* T: Term \(days\) \(e.g. 1 days, 14 days, 30 days …\)
* R: Annual interest rate 

### 7. Prepayment

Prepayment is the early repayment of a loan by the Borrower. No partial repayment is allowed. 

If the Borrower decides to pay off the loan early, aside from the normal interest he has to pay until that point, he will be charged a prepayment penalty \(which is equal to half of the interest he would have had to pay from that point till the maturity date\).

The prepayment interest is calculated as follows:

$$
I = F * R * \frac{T_1 + T}{2*365}
$$

* I: Interest
* F: The original loan amount
* T: Term \(days\) \(1 days, 30 days …\)
* T1: The number of days borrowed.
* R: Annual Interest rate

### 8. Trade

#### **8.1. Status:**

* Open trades
* Liquidated trades
* Closed trades

The status of a trade will be updated from “Open” to “Liquidated” if:

* The market value of the collateral falls to the liquidation value \(see Section 4. Liquidation for more detail\), or
* The Borrower fails to repay the loan by the due date

The status of a trade will be updated from “Open” to “Closed” if the Borrower repays the loan by the due date.

#### 8.2. Jobs

Open trades will be scanned and processed at every 100th block of every epoch. The job will perform the following:

* Liquidation
* Auto top-up
* Auto repay

**8.2.1. Recall excess**

* Recall Rate: 200% \(By default\)

By default, TomoX will support recall excess automatically. Currently, TomoX does not support recall excess manually.

The collateralized asset will be recalled as an amount to the Borrower’s wallet if the market price of the collateralized asset rises to be above the Recall Price.

* Recall Price = Liquidation Price \* Recall Rate
* New Liquidation Price = collateral Price \* liquidation rate / deposit rate
* New Locked Amount =  Old Locked Amount \* \( Old Liquidation Price/New Liquidation Price\) 

Recall Rate is set/adjusted by Moderator.  


**8.2.2.Top Up**

Allows the Borrower to deposit more collateral into the loan.

**8.2.3. Auto Top-Up**

By default, TomoX will automatically top up additional collateral from the Borrower’s wallet if the market price of the collateral falls to or below the liquidation price. 

The amount of the Top-Up will be calculated by the following formula to make sure the new liquidation price is equal to 90% of the market price of the collateralized asset.  


* New Liquidation Price = 90% Current Collateral Market Price
* New Locked Amount =  Old Locked Amount \* \( Old Liquidation Price/New Liquidation Price\) 
* TopUp Amount = New Locked Amount - Old Locked Amount 

**8.2.4. Auto Renew**

NOT supported

#### **8.2.5. Repay**

The Borrower has to repay the value of the loan and the interest of the loan to the Lender by the due date.

**8.2.6.  Auto Repay**

By default, if the Borrower has enough balance of the borrowed asset, TomoX will automatically repay the loan on the due date. 

{% hint style="info" %}
Relayer fees: Fees that relayers must pay the Masternode network. These fees will be automatically deducted from the \*Trading Fee Fund when successfully matched. 

The 25,000 TOMO deposit of the Relayer Owner will be divided into 2 parts:

* Locked Funds: 20,000 TOMO will be locked and only be available for withdrawal 30 days after the relayer owner makes a decision to resign. 
* Trading Fee Fund: 5,000 TOMO will be used for paying network fees, and be deducted from as fees are sent to masternodes for handling trades and order processing
{% endhint %}

