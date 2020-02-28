---
description: Here are the base requirements for running a Masternode Candidate.
---

# Requirements

### Minimum hardware requirements <a id="hardware"></a>

Processing transactions is mostly CPU bound. Therefore we recommend running CPU optimized servers.

* Directly facing internet \(public IP, no NAT\)
* 16 cores CPU
* 32GB of RAM
* SSD storage

{% hint style="info" %}
Note

If you are running a node in Testnet, 2CPU/8GB of RAM is sufficient.
{% endhint %}

We recommend using popular cloud providers as there reliability and uptime are close to 100%. These servers would be a good starting point:

* **DigitalOcean**: CPU optimized droplet 32GB/16CPU
* **Amazon EC2**: C5 instance
* **Google Cloud Engine**: n1-highcpu-16

Setting up a Masternode Candidate on a weaker machine might result in poor performances. Significantly impacting owner's rewards and the chain performance.

If you have other production grade environment than cloud provider at your disposal, please come chat with us on our [Gitter](https://gitter.im/tomochain).

{% hint style="info" %}
Info

A Masternode have a certain amount of tasks to process \(validations, block creations, etc.\) over time. Your Masternode should be able to process all the tasks that are designated to it, or the rewards will be negatively impacted. However, oversizing your asternode will not earn you more rewards.
{% endhint %}

### Maintenance <a id="maintenance"></a>

All IT systems require maintenance.

It is of the owner's responsibility to ensure over time that your node has enough:

* Disk space to store the new blockchain data
* Processing power to keep the chain operating at optimal speed
* Monitoring to be able to react quickly in case of a problem occurring
* Security measures like firewalling, OS security patching, SSH via keypairs, etc.

This is a non exhaustive list.

