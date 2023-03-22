---
description: >-
  Once your full node is up and running, you need to apply to make it eligible
  as a Masternode.
---

# Apply Your Node

Masternodes will receive a significant amount of block rewards, which likely exceeds the cost for running the infrastructure. However, Masternode Candidates need to invest in TomoChain by depositing at least 50,000 TOMO, and stake them for the long term. Furthermore, after the initial deposit to become a candidate, if the Masternode Candidate is not one of the top 150 most voted Candidates, it will not be promoted to Masternode status, and thus receive no rewards. Therefore, Candidates have an incentive to do as much as they can such as signalling their capability to support TomoChain to get into the top 150 most voted Candidates.

### Requirements <a href="#requirements" id="requirements"></a>

To have a Masternode Candidate, the following requirements must be satisfied:

* The token holder has an up and running node - see our [documentation.](run-a-full-node/)
* The token holder must hold a minimum required amount of tokens (50,000 TOMO). These 50,000 TOMO are deposited to the Voting Smart Contract.
* Must be one of the 150 most voted Masternode Candidates in the system. The voting by token holders is credited through a Voting Dapp that allows token holders to send TOMO through the smart contract mechanism.

### Apply to become a Masternode <a href="#applying-to-become-a-masternode" id="applying-to-become-a-masternode"></a>

You can apply to become a Masternode by going on [TomoMaster](https://master.tomochain.com/). Connect the wallet that contains the funds you want to deposit.

{% hint style="danger" %}
Warning

The wallet who makes the initial deposit will be the one receiving block rewards.
{% endhint %}

On the top right corner, click on "Become a Candidate".

Enter the amount of TOMO you want to deposit (minimum 50,000).

Enter your coinbase address. This is the address of the account that your Masternode is using. If your are running your node with `tmn`, you can simply run `tmn inspect` to get it.

{% hint style="warning" %}
Important note:

We advise for security measures to use a fresh new account for your Masternode or 'coinbase address'. This is not the account that will receive the rewards. The rewards are sent to the account that will make the 50,000 TOMO initial deposit.
{% endhint %}

Confirm with apply and proceed to make the payment.

Your full node will now be listed on TomoMaster. People can view its details and vote for it.

A Candidate becomes a Masternode when it belongs to top 150 most voted Candidates in each epoch.

{% hint style="info" %}
Info

An epoch is a period of 900 blocks (\~ 30 minutes) starting from block #1
{% endhint %}

If your node is in the top 150 most voted Candidates at the checkpoint between two epochs, it will be promoted as a Masternode and will start producing blocks at the next epoch.

### Resigning a Masternode <a href="#resigning-your-masternode" id="resigning-your-masternode"></a>

In case you want to stop your node, you need to resign it from the governance first in order to retrieve the locked funds. Access TomoMaster, go to your Candidate detail page, and click the `Resign` button. Your funds will be available to withdraw 30 days after the resignation (1,296,000 blocks).

After resigning successfully, you can stop your node. If you ran it with `tmn`, simply run:

```
tmn remove
```

At this point, your Masternode is completely terminated.
