---
description: Slashing Masternodes to keep the network functionality efficient
---

# TomoChain Slashing Mechanism

With Slashing v2.0, a Masternode who doesn't create any block within an epoch and therefore delays the network by 10 seconds at each of their turns will be penalized \(no rewards\) for the next five epochs.

{% hint style="info" %}
Note: a slashed Masternode can still sign transactions if he’s online but receive no rewards for doing so.
{% endhint %}

After being slashed for 5 epochs, the Masternode is analysed for re-entry. If the slashed Masternode have signed any transaction during the last epoch \(meaning that he's up and working again\) it will come back to its Masternode status and receive rewards normally. Otherwise it will be slashed for a new round of 5 epochs. This can happen as long as the node isn't back up or kicked out of the top 150.

Some reasons for being Slashed might be that the Masternode does not have the correct TomoChain software, lack of memory or Masternode crashes due to the lack of e-maintenance and operation by the Masternode owner.

{% hint style="info" %}
On TomoMaster, click on a candidate to open the candidate page. Scroll down to 'Masternode Rewards'. You should look at 'Sign number', 'Slashing history' under Masternode Rewards to determine a good node or not.
{% endhint %}

Masternodes will sign a maximum of 60 blocks per epoch. A good Masternode will create around 60 sign transactions in that epoch. We also calculate the reward based on sign transactions number.  
  


