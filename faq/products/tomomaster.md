# TomoMaster

## **General**  &#x20;

### **What is TomoMaster?**

[TomoMaster](https://master.tomochain.com/), the 'Governance Dapp', provides a professional UI that lists all Masternodes and Masternode Candidates. Users can vote for Masternodes, see Masternode performance statistics, and deposit 50K TOMO to become a Masternode Candidate.

### **How do I login on TomoMaster?**

Go to [TomoMaster](http://master.tomochain.com). On the top-right corner click 'Login'. Then select how you want to login: with TomoWallet, with Ledger, with Trezor, with Metamask, TrustWallet or Private Key/Mnemonic.

### **What is the 'capacity' of a Candidate/Masternode?**

The capacity of a candidate is the 50K TOMO initial deposit plus the total amount of TOMO voted for that candidate.

### **Which of these numbers on TomoMaster will tell us which is a good performing node vs poorly performing?**

On TomoMaster, click on a candidate to open the candidate page. Scroll down to 'Masternode Rewards'. You should look at 'Sign number', 'Slashing history' under Masternode Rewards to determine a good node or not.

Masternodes will sign a maximum of 60 blocks per epoch. A good Masternode will create around 60 signed transactions in that epoch. The rewards are also calculated based on the number of signed transactions.

### **What is a 'checkpoint'?**

For each iteration of 900 blocks (called epoch), a checkpoint block is created. Afterwhich the rewards are released to Masternodes and Voters. The Masternodes take turns in sequential order to create blocks, verify all of the created blocks in the epoch and count the number of signatures.

It is worth noting that token holders who unvote before the checkpoint block will not receive any shared reward when staking rewards are allocated.

### **I want to stop running my node.**

In case you want to stop your node, you need to resign it from the governance first in order to retrieve your locked funds. Access TomoMaster, go to your candidate detail page, and click the `Resign` button. Your funds will be available to withdraw 30 days after the resignation (1,296,000 blocks).&#x20;

After resigning successfully, you can stop your node. If you ran it with `tmn`, simply run:

```
tmn remove
```

At this point, your Masternode is terminated.

## Features

### Network Status

On TomoMaster, this area shows you what the current block is, the block time, how many blocks are in each epoch, and the next checkpoint (end of epoch).

#### Candidates List <a href="#candidates-list" id="candidates-list"></a>

The candidates list includes every Masternode with enough deposited tokens to run a Masternode, as well as those who resigned running a Masternode. A candidate is required to be one of the top 150 most voted Masternode candidates on this list to become a Masternode to earn rewards. Voters can use this list to help choose which Masternode candidate(s) they would like to stake their tokens to.

`Tip: Voting for the top voted masternode candidate could lower your rewards as the rewards that go to voters per token is inversely proportional to the number of tokens staked for a specific masternode.`

#### Voting <a href="#voting" id="voting"></a>

Voters who want to stake their tokens to a Masternode should simply click ‘Vote’ on the respective Masternode and follow the instructions presented.

#### Unvoting <a href="#unvoting" id="unvoting"></a>

If you do not want to support a Masternode you voted for, you can unvote from it by clicking the Unvote button on the Masternode's page and enter the amount of TOMO you want to unvote.

`Warning: After unvoting, your TOMO will be locked in the smart contract for 48 hours before you are able to withdraw.`

### [Candidate](https://master.tomochain.com/candidate/0x3e3d98a26deef510b720967f4c4dbc88f308a994) <a href="#candidate" id="candidate"></a>

#### General Information <a href="#general-information" id="general-information"></a>

On the top of the page, you can find general information on a Masternode Candidate. Voters can use this information to better understand the Masternode Candidates they plan to vote for.

#### Metrics <a href="#metrics" id="metrics"></a>

The metrics area shows the performance of the Masternode. This section is useful to see if the Masternode Candidate is performing well.

#### Rewards <a href="#rewards" id="rewards"></a>

The rewards section shows the estimated rewards the Masternode has been receiving. If the Masternode has been receiving fewer rewards than other Masternodes, there may be performance issues.

#### Voters <a href="#voters" id="voters"></a>

Under the section for voters, you can see the list of TOMO stakers who have voted for this candidate.

#### Transactions <a href="#transactions" id="transactions"></a>

In this section, you can see all transactions of this candidate.

### [Voter](https://master.tomochain.com/voter/0x82d83629f48b690226af91547cbfbfc8a52b73e6) <a href="#voter" id="voter"></a>

#### General Information <a href="#general-information_1" id="general-information_1"></a>

On this page you can find general information about specific voters.

Tip: As a voter, use this page to make sure you're earning your fair share of rewards.

#### Candidates <a href="#candidates" id="candidates"></a>

The candidates section shows all Masternode Candidates that have been voted by this voter.

#### Rewards <a href="#rewards_1" id="rewards_1"></a>

The rewards section shows the rewards the voter has been receiving.

`Tip: If you voted an equal amount of TOMO for different masternodes and you see one is giving fewer rewards, you may have voted for a masternode with performance issues and should consider changing your vote.`

#### Transactions <a href="#transactions_1" id="transactions_1"></a>

This section shows all transactions by the voter.

### [Settings](https://master.tomochain.com/setting) <a href="#settings" id="settings"></a>

#### Network Provider <a href="#network-provider" id="network-provider"></a>

Use settings to select the network provider you are using for TomoMaster (e.g., Metamask, TomoChain Testnet, Custom Network).

#### Account Info <a href="#account-infos" id="account-infos"></a>

This section will show you information about your public address and TOMO balance.

### [Apply](https://master.tomochain.com/apply) <a href="#apply" id="apply"></a>

This web page is used by TOMO holders looking to apply to become a Masternode Candidate.

### Search <a href="#search" id="search"></a>

On the top of the page, you can find a search bar. You can use this bar to search for a Candidate or Voter by their respective addresses.

`Tip: The search will not work if your input is not an address.`
