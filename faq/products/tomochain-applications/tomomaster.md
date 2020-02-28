# TomoMaster

## **General**   

### **What is TomoMaster?**

[TomoMaster](https://master.tomochain.com/), the 'Governance Dapp', provides a professional UI that allows to see the list of masternodes and candidates, to deposit 50k TOMO to become a masternode candidate, to vote for masternodes, and to show masternode performance statistics.

### **How do I login on TomoMaster?**

Go to [TomoMaster](http://master.tomochain.com). On the top-right corner click 'Login'. Then select how do you want to login: with TomoWallet, with Ledger, with Trezor, with Metamask, TrustWallet or Private Key/Mnemonic.

### **What is the 'capacity' of a Candidate/Masternode?**

The capacity of a candidate is the 50K TOMO initial deposit plus the total amount of TOMO voted for that candidate.

### **Which of these numbers on TomoMaster will tell us which is a good performing node vs poorly performing?**

On TomoMaster, click on a candidate to open the candidate page. Scroll down to 'Masternode Rewards'. You should look at 'Sign number', 'Slashing history' under Masternode Rewards to determine a good node or not.

Masternodes will sign a maximum of 60 blocks per epoch. A good masternode will create around 60 sign transactions in that epoch. We also calculate the reward based on sign transactions number.

### **What is a 'checkpoint'?**

For each iteration of 900 blocks \(called epoch\), a checkpoint block is created, which implements only reward works. The masternode, who takes turn in the circular and sequential order to create blocks, has to scan all of the created blocks in the epoch and count number of signatures.

It is worth noting that token holders who unvote before the checkpoint block will not receive any shared reward in the Staking Reward portion.

### **I want to stop running my node.**

In case you want to stop your node, you need to resign it from the governance first in order to retrieve your locked funds. Access TomoMaster, go to your candidate detail page, and click the `Resign` button. Your funds will be available to withdraw 30 days after the resignation \(1,296,000 blocks\). 

After resigning successfully, you can stop your node. If you ran it with `tmn`, simply run:

```text
tmn remove
```

At this point, your masternode is completely terminated.

## Features

### Network Status

On TomoMaster, this area shows you what the current block is, the block time, how many blocks are in each epoch, and the next checkpoint \(end of epoch\).

#### Candidates List <a id="candidates-list"></a>

The candidates list includes everyone who has deposited enough tokens to run a masternode as well as those who resigned running a masternode. A candidate is required to be one of the top 150 most voted masternode candidates on this list to become a masternode earning rewards. Voters can use this list to help choose which masternode candidate\(s\) they would like to stake their tokens for.

`Tip: Voting for the top voted masternode candidate could lower your rewards as the rewards that go to voters per token is inversely proportional to the number of tokens staked for a specific masternode.`

#### Voting <a id="voting"></a>

Voters who want to stake their tokens for a masternode or masternodes in order to earn rewards can vote through TomoMaster. Simply click ‘Vote’ and you will be taken to a page that allows you to vote through staking your tokens.

#### Unvoting <a id="unvoting"></a>

If you do not want to support a masternode you voted for, you can unvote it by clicking the Unvote button on the masternode's page and enter the amount of TOMO you want to unvote.

`Warning: After unvoting, your TOMO will be locked in the smart contract for 48 hours before you are able to withdraw.`

### [Candidate](https://master.tomochain.com/candidate/0x98ffa09ae64a3ad63289ee0def385e6455b777e5) <a id="candidate"></a>

#### General Information <a id="general-information"></a>

On the top of the page, you can find general information on a masternode candidate. Voters can use this information to better understand the masternode candidates they plan to vote for.

#### Metrics <a id="metrics"></a>

The metrics area shows the performance of the masternode. This section is useful to see if the masternode candidate is strong or weak.

#### Rewards <a id="rewards"></a>

The rewards section shows the estimated rewards the masternode has been receiving. If the masternode has been receiving less rewards than other masternodes, it might be a weak masternode.

#### Voters <a id="voters"></a>

Under the section for voters, you can see the list of TOMO stakers who voted for this candidate.

#### Transactions <a id="transactions"></a>

In this section, you can see all transactions of this candidate.

### [Voter](https://master.tomochain.com/voter/0x82d83629f48b690226af91547cbfbfc8a52b73e6) <a id="voter"></a>

#### General Information <a id="general-information_1"></a>

On this page you can find general information about specific voters.

Tip

As a voter, use this page to make sure you're earning your fair share of rewards.

#### Candidates <a id="candidates"></a>

The candidates section shows all masternode candidates that have been voted by this voter.

#### Rewards <a id="rewards_1"></a>

The rewards section shows the rewards the voter has been receiving.

`Tip: If you voted an equal amount of TOMO for different masternodes and you see one is giving less rewards, you may have voted for a weak masternode and should consider changing your vote.`

#### Transactions <a id="transactions_1"></a>

This section shows all transactions by the voter.

### [Settings](https://master.tomochain.com/setting) <a id="settings"></a>

#### Network Provider <a id="network-provider"></a>

Use settings to select the network provider you are using for TomoMaster \(e.g., Metamask, TomoChain Testnet, Custom Network\).

#### Account Infos <a id="account-infos"></a>

This section will show you information about your public address and TOMO balance.

### [Apply](https://master.tomochain.com/apply) <a id="apply"></a>

This web page is used by TOMO holders looking to apply to become a masternode candidate.

### Search <a id="search"></a>

On the top of the page, you can find a search bar. You can use this bar to search for a Candidate or Voter by its address.

`Tip: The search will not work if your input is not an address.`

