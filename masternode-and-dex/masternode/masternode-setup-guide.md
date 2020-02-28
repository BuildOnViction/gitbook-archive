---
description: >-
  This is a procedural step-by-step guide to setting up your first TomoChain
  Masternode using the tmn tool. It is meant for first-time and
  intermediate-level Masternode operators.
---

# Masternode Setup Guide

Security Disclaimer: Despite there being mention of some security elements in this guide, there is **no implied guarantee of security**. You alone must fully secure your server.

### Technical Requirements / Recommendations <a id="technical-requirements-recommendations"></a>

The following are required items and server specifications. [Click here for more details](requirements.md)

* 50,000 TOMO deposit
* Server \(cloud-VPS or your-own\)
  * 16 vCPU cores \(Prefer higher clock speed. Usually found on "CPU optimized" cloud providers' servers\)
  * 32GB RAM
* Storage \(Disk Space\)
  * 100 GB of storage for the base chaindata
  * ~1 GB of weekly data storage space increase \(reccomend SSD-based Block Storage; low-latency, not NAS speeds\)
  * Note: These numbers may decrease with ongoing optimisations to the code base.
* 2 TomoChain wallets \(addresses\) - [see details below](https://tomochain.gitbook.io/tomochain-docs/masternode-and-dex/masternode/masternode-setup-guide/#7-create-wallet-addresses)

### Knowledge Requirements <a id="knowledge-requirements"></a>

* **VPS Setup** - You are able to setup your own cloud-hosted virtual private server \(VPS\)
* **Linux familiarity** - You have a basic knowledge of how to SSH-into \(ex: putty or terminal\) and operate the Linux command-line.

**Do not proceed if you are not confident** with the Linux command-line. Why? The upkeep and troubleshooting will become more complex than this guide. Some commands fail and you must know what you are doing.

#### For Advanced users, go here \(Command-line-only-version\) <a id="for-advanced-users-go-here-command-line-only-version"></a>

For advanced users or repeat-offenders, see this super-short command-line-only version of the lengthy guide below. If you have done this before or know what you are doing, you might more-easily follow these Linux commands instead of having to read through the lengthy prose below.

> Note: You will _MISS_ many tips and tricks found in the detailed instructions.

#### Beginner/Intermediate users, keep reading... <a id="beginnerintermediate-users-keep-reading"></a>

### Introduction <a id="introduction"></a>

#### What is a Masternode? <a id="what-is-a-masternode"></a>

A Masternode is a computer on a decentralized blockchain network that is running 24 hours a day, and keeps the system operational. It powers the blockchain network by processing transactions and signing blocks.

#### What are the benefits of a asternode? <a id="what-are-the-benefits-of-a-masternode"></a>

Masternodes help support the network by creating and signing blocks, providing faster transaction times, and decentralized operations. They utilize PoS \(Proof of Stake\) vs PoW \(Proof of Work\) consensus-building. Masternode operators are paid a reward \(tokens\) as an incentive for their involved investment of token deposit, server setup, and continued operation.

#### What is a VPS? <a id="what-is-a-vps"></a>

VPS stands for Virtual Private Server. They are paid servers hosted on a cloud-hosting-provider. Each VPS runs an independent installation of an operating system \(OS\), Linux or Windows, and typically provides root access to the OS for advanced management and control.

#### Why is a VPS highly recommended for Masternodes? <a id="why-is-a-vps-highly-recommended-for-masternodes"></a>

A VPS is recommended \(and often required\) for asternode setups, as you will need a dedicated static IP and 99.9% uptime to provide a stable and efficient node for the network. Unlike your home or office PC, a Masternode VPS serves one purpose, to securely and efficiently run a asternode. A VPS is online 24/7 and provides dedicated resources for the project’s decentralized network.

### 1. Choose your hosting provider <a id="1-choose-your-hosting-provider"></a>

Choose which VPS hosting provider you want to utilize.

The following providers are **sample** VPS providers. You could choose elsewhere, or even your own 24/7 server.

* [AWS \(Amazon\)](https://aws.amazon.com/)
* [DigitalOcean](https://www.digitalocean.com/)
* [GCE \(Google\)](https://cloud.google.com/compute/)
* [Linode](https://www.linode.com/)
* [OVH](https://www.ovh.com/)
* [Vultr](https://www.vultr.com/)

> Note on provider choice: It is encouraged for asternode operators to utilize various hosting providers so as to encourage a more decentralized network. It is in your best interest because if any one popular provider goes down, others will get more rewards.

### 2. Start your VPS server <a id="2-start-your-vps-server"></a>

**Start/Boot your VPS server instance.**  
Choose **Ubuntu 18.04**. This is an LTS version \([Long Term Support](https://wiki.ubuntu.com/LTS)\). LTS versions are more stable and have seen less errors when installing Docker and Python. You must use Ubuntu 18.04 to seek support from the wider community or TomoChain. If you need help with this, [see this example](https://medium.com/tomochain/how-to-run-a-tomochain-masternode-from-a-to-z-3793752dc3d1#6122).

> Data Storage: It is recommended to assure that your provider has Block Storage or expandable disk space on SSD drives \(more performant\). Block Storage is pay-as-you-go disk space that you can expand in the future. You may not need it now, but you will in the future. Some locations within a hosting provider do not have this, while others will.
>
> SSH-Key login: Consider utilizing a **SSH-Key login** over passwords. Some providers allow you to set it up upon server creation.

### 3. Change passwords and accounts \(logged in as root user\) <a id="3-change-passwords-and-accounts-logged-in-as-root-user"></a>

Login to your newly created server with SSH / Putty.  
If you need help with this, [see this example](https://medium.com/tomochain/how-to-run-a-tomochain-masternode-from-a-to-z-3793752dc3d1#20a7).

```text
SSH root@178.62.127.177
```

> Note on Users: Login as the `root` user at first. Later, we will create and switch to your own username.

If you did not utilize SSH-key login \(highly recommended\), you will want to change the root password \(only the first time\) with the following command.

```text
passwd
```

> Save your root password as you can get locked out of your own server if you forget it. It is strongly recommended to use a 16+ char password with a mix of letters, numbers, special characters.

You are now logged in as root. The root user is the administrative user in a Linux environment that has very broad privileges. Because of the heightened privileges of the root account, you are _discouraged_ from using it on a regular basis. This is because part of the power inherent with the root account is the ability to make very destructive changes, even by accident.

The next step is to [set up an alternative user account](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04) with a reduced scope of influence for day-to-day work.

#### Create a new user <a id="create-a-new-user"></a>

Use the following command to add a new user account that we will use to log in to from now on. Our user is called Michael, you can replace it with any username that you like. Use the same username as your local mac/PC username and you will have an easier time logging in!

```text
adduser michael
```

You will be asked a few questions, starting with the account password. Enter a strong password. Optionally, fill in any of the additional information if you want or ignore it. This is not required and you can just hit ENTER in any field you wish to skip.

#### Grant the user administrative privileges <a id="grant-the-user-administrative-privileges"></a>

Now we have a new user account with regular account privileges. However, we will need to do administrative tasks from this normal account.

To add these privileges to our new user, we need to add the new user to the **sudo** group. This will allow our normal user to run commands with _administrative privileges_ by putting the word `sudo`before each command.

As root, run this command to add your new user to the sudo group \(substitute Michael with your new user\):

```text
usermod -aG sudo michael
```

> -a stands for Append and -G is Group; sudo is the group name you are adding to your user

You can check to make sure that the usermod command worked:

```text
cat /etc/group | grep sudo
groups michael
```

Assure that you get a response such as `sudo:x:27:michael` from first command and `michael : michael sudo` from the second command. 

When you eventually \(not yet\) log in as your new user, you can type `sudo` before commands to perform actions with superuser privileges. Remain logged in as the root user for now, as we have more initial setup to do. After this, you will almost always login as your new user.   
  


### 4. Configure your VPS \(remain logged in as root user\) <a id="4-configure-your-vps-remain-logged-in-as-root-user"></a>

We will now prepare the [prerequisites for tmn](https://docs.tomochain.com/get-started/run-node/). You need Python 3.6+ and Docker installed.

#### Upgrade operating system <a id="upgrade-operating-system"></a>

We should upgrade the Ubuntu operating system and all installed package libraries first. You may consider doing this upgrade occasionally in the future. Type these two commands on the console with an ENTER after each:

```text
apt update
apt upgrade
```

> Watch out for WARNINGs or ERRORs. A lot of text could fly by, and you should watch all of it in case something installs incorrectly. Google anything out of the ordinary and try to understand or fix it.

Reboot your VPS instance in case any of the upgraded components will only fully engage until rebooted fresh.

```text
reboot
```

#### Install Python <a id="install-python"></a>

```text
apt install python3
apt install python3-pip
```

Check if you have installed the right Python version \(must be newer than version 3.6\).

```text
python3 --version
```

#### System Security <a id="system-security"></a>

This topic is optional, but highly recommended. If the default SSH port is not changed, you could see nefarious connection-attempts in a short time-period.

[Look at our wiki security doc for more details](https://github.com/tomochain/docs/wiki/Security-of-Masternodes)

At a minimum, you will want to consider:

* SSHD on non-standard port
* UFW \(Uncomplicated Fire Wall\) \(open port 30303 tcp & udp, and above non-standard SSH\)

Other security options you could consider:

* SSH key-based login \(vs password\)
* Fail2ban
* Blocking remote password auth
* Blocking remote root SSH-access 

### 5. Setup Docker \(logged in as new user\)

From now on, you will almost always want to login as your **new user**. If you are logged in as root still, logout and log back in as the new user. You may want to consider denying remote root SSH logins.

```text
SSH michael@178.62.127.177
```

#### Install Docker Repositories <a id="install-docker-repositories"></a>

Update the apt package index. Then install various packages to allow apt to use a repository over HTTPS. The third line adds Docker’s official GPG key.

```text
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

> "OK" is normal output of that last command; -fsS shows less progress, but still error messages and -L allows redirect
>
> NOTE: Be careful with certain SSH consoles. They may not paste the ‘\|’ symbol correctly.

Next, verify that you have the correct key, by searching for the last 8 characters of the fingerprint. Compare the results to what is below.

```text
apt-key fingerprint 0EBFCD88
```

Example Results \(format may be slightly different, but the string of char-numbers the same\):

```text
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```

Use the following command to set up the "stable" repository. You could get errors here if you have a release of Ubuntu that is too recent \(non LSB\).

```text
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

#### Install Docker CE <a id="install-docker-ce"></a>

Update the apt package index. Then install the latest version of Docker CE:

```text
sudo apt update
sudo apt install docker-ce
```

> Watch out for WARNINGs or ERRORs. Google anything out of the ordinary and try to understand or fix it.

Once installed, add your current user to the Docker group and verify that the user has been added.

```text
sudo usermod -aG docker michael
groups michael
cat /etc/group | grep docker
```

#### Assure Docker is working <a id="assure-docker-is-working"></a>

Verify that Docker CE is installed correctly by running the hello-world image. This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits. The second command shows more detailed docker information.

```text
docker run hello-world
sudo systemctl status docker  # hit 'q' to exit
```

**Docker CE is installed and running.**

Congratulations! You have installed Python and Docker. You have the prerequisites ready to run TomoChains' tmn.

TROUBLESHOOTING

error: could not access the docker daemon

If you have installed Docker, and get this error, you probably forgot to add your user to the docker group. Please run this, close your session and open it again.

`usermod -aG docker $(whoami)`

### 6. Installing TMN utility <a id="6-installing-tmn-utility"></a>

`Tmn` is a simple interface created by TomoChain developers to **help you quick start your asternode**. It is installed as a python package and it utilizes two docker containers once operating. We will follow through the steps found here: [guide to install tmn](https://docs.tomochain.com/get-started/run-node/)

> “We made a simple command line interface called tmn to easily and quickly start a TomoChain Masternode. It takes care of starting the necessary docker containers with the proper settings for you. It will really suit you if you don’t already have a big infrastructure running. Spin up a machine in your favorite cloud and get your asternode running in a few minutes!”

Install and update the tomochain-created `tmn` utility from pip:

```text
pip3 install --user tmn
pip3 install -U tmn
```

> Watch out for WARNINGs or ERRORs and troubleshoot \(see end of this section\).

To check that `tmn` has been correctly installed, use the following command to show some tmn info:

```text
pip3 show tmn

Name: tmn
Version: 0.5
Summary: Quickstart your masternode
Home-page: https://tomochain.com
Author: Etienne Napoleone
Author-email: etienne@tomochain.com
License: GPL-3.0+
Location: /home/michael/.local/lib/python3.6/site-packages
Requires: python-slugify, click, clint, pastel, docker
```

The next step will be to actually **START TMN**, however we cannot do this until we have two wallet addresses. See the next section for this.

TROUBLESHOOTING

Occasionally a VPS image will not come installed with all of the software packages needed to install what we need. If you get any of the errors below, you are in need of particular packages to be installed.

```text
ERROR:
ModuleNotFoundError: No module named ‘setuptools’
SOLUTION:
sudo apt-get install python3-setuptools
```

```text
ERROR:
Failed building wheel for <package>
SOLUTION:
pip3 install wheel
```

```text
ERROR:
error: command 'x86_64-linux-gnu-gcc' failed with exit status 1
SOLUTION:
sudo apt install build-essential
```

```text
ERROR:
fatal error: Python.h: No such file or directory
SOLUTION:
sudo apt install python3-dev
```

### 7. Create Wallet Addresses <a id="7-create-wallet-addresses"></a>

Before being able to proceed further, you will need **two** seperate TOMO wallet addresses to operate a Masternode. One helps to operate the Masternode day-to-day, and the other is where the 50,000 TOMO is staked from. The genius of this is that the wallet where the 50,000 TOMO will pass through \(and where rewards will eventually come into\) is never stored or seen by the VPS server. This is a security strategy that keeps your coins safe.

> WALLET1 - Operating Wallet: Used for operating the Masternode, including signing blocks. It effectively acts as a unique identifier of your Masternode. No coins need to be inserted in this wallet; It's even advised to be empty, so in case of breach, no funds are exposed.
>
> WALLET2 - Deposit Wallet: Your 50,000 of staked tokens need to be placed here; later, the 50,000 will go into a smart contract; eventually, Masternode rewards will show here.

You will need both the **Public Key** and **Private Key** for both addresses. It is advise that you store all of this information somewhere safe, yet accessible. You may need to utilize this information during continued operations of your Masternode. Password manager apps like KeePass/KeePassXC, LastPass, or 1Password are your friend. Your private key is your money. Give it to no one.

* WALLET1 Suggestions - If setting up a single Masternode, you can use a mobile wallet. Binances `Trust Wallet` and TomoChains `Tomo Wallet` apps are best. Alternatives are Metamask and MEW \(MyEtherWallet\), in that order. You can use Ledger Hardware Wallet, however the added security on WALLET1 isn't as necessary.
* WALLET2 Suggestions - Preferred to use Ledger / Hardware Wallet \(if possible\) in combo with Metamask because 50,000 and rewards will be handled here. Assure to use an address you do not have history on eth chain with - otherwise others will be able to see your unrelated investment history.

Because most wallet apps do not have TomoChain mainnet as a selectable network yet, you will need to manually add the new mainnet if you have not already. See the first link below for the guide on how to do this.

How to Set Up a Wallet:

* [Setting Up MyEtherWallet, Metamask, or Binance TrustWallet](https://bit.ly/2A6zrC7)

More info:

* [Using Metamask or Mobile TomoWallet](https://docs.tomochain.com/get-started/wallet/)
* [Old Masternode guide \(testnet\) Section on wallets](https://medium.com/tomochain/how-to-run-a-tomochain-masternode-from-a-to-z-3793752dc3d1#0e58)  

### 8. Run TMN <a id="8-run-tmn"></a>

Below, you will finally start your TomoChain node with a utility called `tmn`.

#### Initial TMN start <a id="initial-tmn-start"></a>

**IMPORTANT:** Logout and SSH back in so that the $PATH variable takes effect. This allows you to run `tmn` from any directory.

```text
exit
ssh michael@178.62.127.177
```

When you first start your full node with `tmn start`, you need to give some information.

> **--name:** The name of your full node. Your input will be converted to a "slugified" name. Slug format allows all letters and numbers, dashes \("-"\) and underscores \("\_"\). Ex: `MyMaStErNode#24 cool` -&gt; `mymasternode24-cool`. You can name it to reflect your identity, company name, etc. 
>
> **--net:** The network your full node will connect to. You can choose here to connect it to the TomoChain `mainnet` or `testnet`. 
>
> **--pkey:** The private key of your WALLET1 wallet \(non 50k\). A TomoChain full node uses a wallet address to be uniquely identified and to receive transaction fees. Transaction fees are not rewards, and they are usually tiny. Important note: we advise for security measures to use a fresh new wallet for your Masternode. This is not the wallet that will receive the rewards. The rewards are sent to the wallet that will make the 50k TOMO initial deposit.

The command is structured like this:

```text
tmn start --name [YOUR_NODE_NAME] --net mainnet --pkey [YOUR_WALLET1_PRIVATE_KEY]
```

We used the following command for our node \(copy your own **name** & **private key**\):

```text
tmn start --name Atlantis --net mainnet --pkey cf03cb58************
```

TROUBLESHOOTING

`tmn: command not found`

It might happen that your PATH is not set by default to include the default user binary directory. You can add it by adding it to your shell $PATH:

On GNU/Linux:

```text
echo "export PATH=$PATH:$HOME/.local/bin" >> $HOME/.bashrc
source $HOME/.bashrc
```

### 9. Check sync status <a id="9-check-sync-status"></a>

This section coming soon.

Contents to come: `tmn status`; `tmn inspect`; `top` command; https://stats.tomochain.com/ website; \# of blocks command; `tmn update`, `tmn --help`, etc   


### 10. Jumpstart the chaindata \(Optional\) <a id="10-jumpstart-the-chaindata-optional"></a>

[Full Jumpstart instructions can be found here](https://github.com/tomochain/docs/wiki/Update-stuck-node-or-Jumpstart-chain-sync)

The basic structure has been created, blocks have started synchronizing, and now we want to speed up the process by pulling in the latest chaindata.

> Chaindata is where the entire history of TomoChain blockchain records are stored. All coin transactions, all smart contracts, all operations. This takes up a _lot_ of space. To syncrhonize it from decentralized nodes piecemeal-like could take days or weeks. Instead, lets download the latest image of the data, and synchronize from there.

### 11. Apply for Masternode Candidacy <a id="11-apply-for-masternode-candidacy"></a>

This section coming soon. [For now, see here](https://docs.tomochain.com/get-started/apply-node/)

Contents to come: Explain; Assure synced; master.tomo; login; apply   


### 12. Name your Masternode <a id="12-name-your-masternode"></a>

This section coming soon.

Contents to come: https://master.tomochain.com/ ; login as 50k wallet; find your MN; edit; enter name; sign data   


### 13. Verify initial rewards <a id="13-verify-initial-rewards"></a>

This section coming soon.

Contents to come: https://master.tomochain.com/ ; https://scan.tomochain.com/ ; explain infra vs stake reward; link to economics

## APPENDIX <a id="appendix"></a>

### Commands-only \(ADVANCED users\) <a id="commands-only-advanced-users"></a>

If you have done this before or know what you are doing, you can follow these Linux commands.

> Note: You will _MISS_ many tips and tricks in the detailed instructions.

```text
ssh root@178.62.127.177
passwd

adduser michael; usermod -aG sudo michael
groups michael

apt update; apt upgrade; reboot

apt install python3
apt install python3-pip
python3 --version

ssh michael@178.62.127.177
sudo apt update; sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update; sudo apt install docker-ce
sudo usermod -aG docker michael; groups michael
docker run hello-world

pip3 install --user tmn
pip3 install -U tmn
pip3 show tmn

# Create Wallet Addresses

# logoff ssh and back in to set $PATH variable
tmn start --name Atlantis --net mainnet --pkey cf03cb58************
tmn status; tmn inspect; tmn --help

# Enact Jumpstart: https://github.com/tomochain/docs/wiki/Update-stuck-node-or-Jumpstart-chain-sync
```

