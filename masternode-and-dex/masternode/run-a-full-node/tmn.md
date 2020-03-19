---
description: >-
  We made a simple command line interface called tmn to easily and quickly start
  a TomoChain Masternode
---

# Tmn

It takes care of starting the necessary docker containers with the proper settings for you. It will really suit you if you don't already have a big infrastructure running. Spin up a machine in your favorite cloud and get your Masternode running in a few minutes!

### Prerequisites <a id="prerequisites"></a>

* [Python](https://docs.python-guide.org/starting/install3/linux/) &gt;= 3.6
* [Docker CE](https://docs.docker.com/install/)

Warning

We recommnd to run your Masternode on Ubuntu 18.04 LTS. This version have python 3.6 and has been reported as working out of the box.

#### Installation of Python <a id="installation-of-python"></a>

To install Python under debian based distribution, run the following commands.

```text
apt update

apt install python3-pip
```

To check if you have installed the right Python version \(must be greater than 3.5\).

```text
python3 --version
```

![tmn python](https://docs.tomochain.com/assets/tmn_python.png)

#### Installation of Docker CE <a id="installation-of-docker-ce"></a>

To install Docker, first update the apt package index.

```text
sudo apt update
```

Then Install packages to allow apt to use a repository over HTTPS.

```text
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

Add Docker’s official GPG key.

```text
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Verify that you now have the key with the fingerprint `9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88`, by searching for the last 8 characters of the fingerprint.

```text
apt-key fingerprint 0EBFCD88
```

![](../../../.gitbook/assets/image%20%2826%29.png)

Set up the stable Docker repository.

```text
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

Update the apt package index. Then install the latest version of Docker CE.

```text
sudo apt update

sudo apt install docker-ce
```

Once installed, add your current user to the Docker group.

```text
usermod -aG docker $your_user_name
```

Warning

You need to relog into your account for this to take effect.

Verify that Docker CE is installed correctly by running the hello-world image:

```text
docker run hello-world
```

This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.

### tmn <a id="tmn"></a>

#### Installation <a id="installation"></a>

Simply install it from pip.

```text
pip3 install --user tmn
```

#### Update <a id="update"></a>

Update it from pip.

```text
pip3 install -U tmn
```

#### First start <a id="first-start"></a>

When you first start your full node with tmn, you need to give some information.

`--name`: The name of your full node. It should be formatted as a slug string. Slug format authorize all letters and numbers, dashes \("-"\) and underscores \("\_"\). You can name it to reflect your identity, company name, etc.

`--net`: The network your full node will connect to. You can choose here to connect it to the TomoChain Testnet or Mainnet.

`--pkey`: The private key of the account that your full node will use. A TomoChain full node uses an account to be uniquely identified and to receive transaction fee.

Important note:

We advise, for security measures, to use a fresh new account for your Masternode. This is not the account who will receive the rewards. The rewards are sent to the account who will make the 50,000 TOMO initial deposit.

`--api`: Expose RPC and websocket on ports `8545` and `8546`.

Important note:

Those ports should not be accessible directly from the internet. Please setup fire-walling accordingly if you need to access them localy. Use a reverse proxy if you want to expose them to the outside.

It could look like this:

```text
tmn start --name [YOUR_NODE_NAME] --net testnet --pkey [YOUR_COINBASE_PRIVATE_KEY] --api
```

Once started, you should see your node on the [stats page](https://stats.testnet.tomochain.com/)!

Note: It can take up to one hour to properly sync the entire blockchain.

![](../../../.gitbook/assets/image%20%2858%29.png)



### Usage <a id="usage"></a>

You can now interact with it via the other commands:

`stop`: Stop your full node.

`start`: Start your full node if it is stopped.

`status`: The current status of your full node.

`inspect`: Display the details related to your full node. Useful for applying your full node as a Masternode.

`remove`: Completely remove your asternode, unique identity and data.

### Troubleshooting <a id="troubleshooting"></a>

#### tmn: command not found <a id="tmn-command-not-found"></a>

It might happen that your PATH is not set by default to include the default user binary directory. You can add it by adding it to your shell $PATH:

On GNU/Linux:

```text
echo 'export PATH=$PATH:$HOME/.local/bin' >> $HOME/.bashrc
```

On MacOS: Replace `[VERSION]` by your version of python \(3.5, 3.6, 3.7\)

```text
echo 'export PATH=$PATH:$HOME/Library/Python/[VERSION]/bin' >> $HOME/.bashrc
```

Then reload your environment:

```text
source ~/.bashrc
```

#### error: could not access the docker daemon <a id="error-could-not-access-the-docker-daemon"></a>

If you have installed Docker, you probably forgot to add your user to the docker group. Please run this, close your session and open it again.

```text
usermod -aG docker $your_user_name
```

#### pip3 install fails due to not being able to build some package <a id="pip3-install-fails-due-to-not-being-able-to-build-some-package"></a>

Your OS might not come with build tools preinstalled.

For ubuntu, you can solve that by running:

```text
sudo apt install build-essential python3-dev python3-wheel
```

#### pip3 install fails due to "No Module named Setuptools" <a id="pip3-install-fails-due-to-no-module-named-setuptools"></a>

Your OS might not come with setup tools preinstalled.

For ubuntu, you can solve that by running:

```text
sudo apt install python3-setuptools
```

