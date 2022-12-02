---
description: >-
  This guide shows how to run a TomoChain Masternode in testnet and mainnet
  without the need of using Docker and tmn.
---

# Binary

### Install Golang <a href="#install-golang" id="install-golang"></a>

* Reference: https://golang.org/doc/install
* Set environment variables
* Supports Go 1.10, 1.11, 1.12

```
export GOROOT=$HOME/usr/local/go
export GOPATH=$HOME/go
```

### Prepare tomo client software <a href="#prepare-tomo-client-software" id="prepare-tomo-client-software"></a>

**Build from source code¶**

Create new directory for the project

```
mkdir -p $GOPATH/src/github.com/tomochain/
cd $GOPATH/src/github.com/tomochain/
```

* Download source code and build

```
git clone https://github.com/tomochain/tomochain.git tomochain
cd tomochain
```

* Checkout the latest version (e.g v2.2.4)

```
git pull origin --tags
git checkout v2.2.4
```

* Build the project

```
make all
```

* Binary file should be generated in build folder `$GOPATH/src/github.com/tomochain/tomochain/build/bin`

```
alias tomo=$GOPATH/src/github.com/tomochain/tomochain/build/bin/tomo
```

**Download TomoChain binary from Github release page**

Download tomo binary from our [releases page](https://github.com/tomochain/tomochain/releases)

```
alias tomo=path/to/tomo/binary
```

### Download genesis block <a href="#download-genesis-block" id="download-genesis-block"></a>

$GENESIS\_PATH : location of genesis file you would like to put

```
export GENESIS_PATH=path/to/genesis.json
```

* Testnet

```
curl -L https://raw.githubusercontent.com/tomochain/tomochain/master/genesis/testnet.json -o $GENESIS_PATH
```

* Mainnet

```
curl -L https://raw.githubusercontent.com/tomochain/tomochain/master/genesis/mainnet.json -o $GENESIS_PATH
```

### Create datadir <a href="#create-datadir" id="create-datadir"></a>

* create a folder to store tomochain data on your machine

```
export DATA_DIR=/path/to/your/data/folder
mkdir -p $DATA_DIR/tomo
```

### Initialize the chain from genesis <a href="#initialize-the-chain-from-genesis" id="initialize-the-chain-from-genesis"></a>

```
tomo init $GENESIS_PATH --datadir $DATA_DIR
```

### Initialize / Import accounts for the nodes's keystore <a href="#initialize-import-accounts-for-the-nodess-keystore" id="initialize-import-accounts-for-the-nodess-keystore"></a>

If you already had an existing account, import it. Otherwise, please initialize new accounts&#x20;

```
export KEYSTORE_DIR=path/to/keystore
```

**Initialize new accounts**

```
tomo account new \
    --password [YOUR_PASSWORD_FILE_TO_LOCK_YOUR_ACCOUNT] \
    --keystore $KEYSTORE_DIR
```

**Import accounts**

```
tomo account import [PRIVATE_KEY_FILE_OF_YOUR_ACCOUNT] \    
    --keystore $KEYSTORE_DIR \
    --password [YOUR_PASSWORD_FILE_TO_LOCK_YOUR_ACCOUNT]
```

**List all available accounts in keystore folder**

```
tomo account list --datadir $DATA_DIR  --keystore $KEYSTORE_DIR
```

### Start a node <a href="#start-a-node" id="start-a-node"></a>

**Environment variables**

* $IDENTITY: the name of your node
* $PASSWORD: the password file to unlock your account
* $YOUR\_COINBASE\_ADDRESS: address of your account which generated in the previous step
* $NETWORK\_ID: the networkId. Mainnet: 88. Testnet: 89
* $BOOTNODES: The comma separated list of bootnodes. Find them [here](https://docs.tomochain.com/developer-guide/working-with-tomochain/tomochain-mainnet#bootnodes)
* $WS\_SECRET: The password to send data to the stats website. Find them [here](https://docs.tomochain.com/developer-guide/working-with-tomochain/tomochain-mainnet#stats-websocket-secret)
* $NETSTATS\_HOST: The stats website to report to, regarding to your environment. Find them [here](https://docs.tomochain.com/developer-guide/working-with-tomochain/tomochain-mainnet#stats-websocket-secret)
* $NETSTATS\_PORT: The port used by the stats website (usually 443)

**Let's start a node**

```
tomo  --syncmode "full" \
    --announce-txs \
    --datadir $DATA_DIR --networkid $NETWORK_ID --port 30303 \
    --keystore $KEYSTORE_DIR --password $PASSWORD \
    --identity $IDENTITY \
    --mine --gasprice 250000000 \
    --bootnodes $BOOTNODES \
    --ethstats $IDENTITY:$WS_SECRET@$NETSTATS_HOST:$NETSTATS_PORT
```

If you are a dapp developer, you should open RPC and WS apis:

```
tomo  --syncmode "full" \
    --announce-txs \
    --datadir $DATA_DIR --networkid $NETWORK_ID --port 30303 \
    --keystore $KEYSTORE_DIR --password $PASSWORD \
    --rpc --rpccorsdomain "*" --rpcaddr 0.0.0.0 --rpcport 8545 --rpcvhosts "*" \
    --rpcapi "db,eth,net,web3,personal,debug" \
    --ws --wsaddr 0.0.0.0 --wsport 8546 --wsorigins "*" --unlock "$YOUR_COINBASE_ADDRESS" \
    --identity $IDENTITY \
    --mine --gasprice 250000000 \
    --bootnodes $BOOTNODES \
    --ethstats $IDENTITY:$WS_SECRET@$NETSTATS_HOST:$NETSTATS_PORT
```

**Some explanations on the flags**

```
--verbosity: log level from 1 to 5. Here we're using 4 for debug messages

--datadir: path to your data directory created above.

--keystore: path to your account's keystore created above.

--identity: your full-node's name.

--password: your account's password.

--networkid: our network ID.

--port: your full-node's listening port (default to 30303)

--rpc, --rpccorsdomain, --rpcaddr, --rpcport, --rpcvhosts: your full-node will accept RPC requests at 8545 TCP.

--ws, --wsaddr, --wsport, --wsorigins: your full-node will accept Websocket requests at 8546 TCP.

--mine: your full-node wants to register to be a candidate for masternode selection.

--gasprice: Minimal gas price to accept for mining a transaction.

--targetgaslimit: Target gas limit sets the artificial target gas floor for the blocks to mine (default: 4712388)

--bootnode: bootnode information to help to discover other nodes in the network

--gcmode: blockchain garbage collection mode ("full", "archive")

--synmode: blockchain sync mode ("fast", "full", or "light". More detail: https://github.com/tomochain/tomochain/blob/master/eth/downloader/modes.go#L24)

--ethstats: send data to stats website

--tomo-testnet: required when the networkid is testnet(89)

--store-reward: store reward report
```

To see all flags usage

```
tomo --help
```

### See your node on stats page <a href="#see-your-node-on-stats-page" id="see-your-node-on-stats-page"></a>

* Testnet: [https://stats.testnet.tomochain.com](https://stats.testnet.tomochain.com/)
* Mainnet: [https://stats.tomochain.com](http://stats.tomochain.com/)

### Troubleshoot <a href="#troubleshoot" id="troubleshoot"></a>

If your node seems run smooth with no error logs but still get slash frequently. You need to check system time on your node, your system time have to be synced from NTP server

E.g:

```
$ timedatectl
Local time: Fri 2019-07-26 05:57:40 CEST
  Universal time: Fri 2019-07-26 03:57:40 UTC
        RTC time: Fri 2019-07-26 03:58:01
       Time zone: Europe/Berlin (CEST, +0200)
 Network time on: yes
NTP synchronized: no
 RTC in local TZ: no
```

`NTP synchronized: no` means your node does not use NTP, you have to enable it.
