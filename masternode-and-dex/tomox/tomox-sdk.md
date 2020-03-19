---
description: >-
  This guide shows how to run a TomoX MongoDb Fullnode. To run the fullnode, you
  need to have MongoDb instance that enable replica set.
---

# Running a TomoX Mongodb Fullnode

### Start MongoDB <a id="start-mongodb"></a>

In this tutorial, we will run a mongo instance with Docker. Run this command:

```text
docker run -d -p 27017:27017 --name mongodb \
    --hostname mongodb mongo:4.2 --replSet rs0
```

Enable Mongodb replica set:

```text
docker exec -it mongodb mongo --eval "rs.initiate()"
```

### Run a fullnode <a id="run-a-fullnode"></a>

Download `tomo` version 2.0+ from [TomoChain Github Release page](https://github.com/tomochain/tomochain/releases)

E.g:

```text
wget https://github.com/tomochain/tomochain/releases/download/v2.1.0-beta/tomo-linux-amd64 -O tomo
chmod +x tomo
sudo mv tomo /usr/bin/
```

Create a coinbase address:

```text
tomo account new
```

Init genesis block: **Testnet**

```text
curl -L https://raw.githubusercontent.com/tomochain/tomochain/testnet/genesis/testnet.json -o genesis.json
tomo init genesis.json
```

Then run the node:

**Testnet**

```text
NODENAME=[your_node_name]
tomo \
    --bootnodes "enode://ba966140e161ad416a7bd7c75dc695e0a41232723e2b19cbbf651883ef5e8f2528801b17b9d63152814d219a58a4fcc3e3c877486e64057523f6714092348efa@195.154.150.210:30301" \
    --networkid 89 \
    --rpc --rpccorsdomain "*" --rpcaddr 0.0.0.0 --rpcport 8545 --rpcvhosts "*" \
    --ws --wsaddr 0.0.0.0 --wsport 8546 --wsorigins "*" \
    --rpcapi "personal,db,eth,net,web3,txpool,miner,tomox" \
    --announce-txs \
    --tomo-testnet \
    --tomox.dbengine "mongodb" \
    --ethstats "${NODENAME}:9tlu4EymcTrEzaqWpSxh3KSa926au8@stats.testnet.tomochain.com"
```

You node will sync the data from TomoChain network, you need to wait until your node catch up the latest block. You can check the status in the logs or the stats page.

To save your time, you should download [chaindata snapshot](https://docs.tomochain.com/masternode/tomox-fullnode/#testnet-chaindata-snapshot) and override your chaindata.

### Troubleshoot <a id="troubleshoot"></a>

**Fatal: Failed to write genesis block**

You already inited genesis block for the default datadir. So you need to use another datadir by `--datadir`

```text
tomo account new --datadir [YOUR_DATADIR]
tomo init genesis.json --datadir [YOUR_DATADIR]
```

### Example <a id="example"></a>

**Testnet**

```text
wget https://github.com/tomochain/tomochain/releases/download/v2.0.0-beta/tomo-linux-amd64 -O tomo
chmod +x tomo
sudo mv tomo /usr/bin/
tomo --version
tomo version
curl -L https://raw.githubusercontent.com/tomochain/tomochain/master/genesis/testnet.json -o genesis.json
tomo init genesis.json 
tomo account new --datadir /tmp/chaindata
tomo init genesis.json --datadir /tmp/chaindata/
NODENAME=testnode02
tomo \
    --bootnodes "enode://ba966140e161ad416a7bd7c75dc695e0a41232723e2b19cbbf651883ef5e8f2528801b17b9d63152814d219a58a4fcc3e3c877486e64057523f6714092348efa@195.154.150.210:30301" \
    --networkid 89 \
    --rpc \
    --rpccorsdomain "*" --rpcaddr 0.0.0.0 --rpcport 8545 --rpcvhosts "*" \
    --ws --wsaddr 0.0.0.0 --wsport 8546 --wsorigins "*" \
    --rpcapi "personal,db,eth,net,web3,txpool,miner,tomox" \
    --announce-txs --tomo-testnet --tomox.dbengine "mongodb" \
    --ethstats "${NODENAME}:9tlu4EymcTrEzaqWpSxh3KSa926au8@stats.testnet.tomochain.com" \
    --datadir /tmp/chaindata/
```

### Testnet chaindata snapshot <a id="testnet-chaindata-snapshot"></a>

To speed up syncing chaindata, you can download chaindata snapshot and override your local chaindata.

Download: [Testnet chaindata](https://chaindata-testnet.s3-ap-southeast-1.amazonaws.com/chaindata-testnet.tar)

E.g:

```text
# Download
wget -c https://chaindata-testnet.s3-ap-southeast-1.amazonaws.com/chaindata-testnet.tar

# Uncompress
tar xvf chaindata-testnet.tar
```

