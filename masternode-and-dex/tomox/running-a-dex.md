---
description: This guide will show how to start a TomoX DEX on your server.
---

# Running a TomoX DEX

To start, download the TomoX-SDK source code which includes two parts:

* [TomoX-SDK](https://github.com/tomochain/tomox-sdk): Backend server, API. It requires Mongodb database with rabbitmq.
* [TomoX-SDK-UI](https://github.com/tomochain/tomox-sdk-ui): Frontend - DEX UI. It requires NodeJs, React

To enable trading for the DEX, register the DEX on TomoRelayer by depositing 25K TOMO.

### Quick start <a href="#quick-start" id="quick-start"></a>

Run this command on an empty server Ubuntu version 16+ to **install** or **update** your DEX:

```
bash <(curl -sSL https://tomochain.com/get-tomox.sh)
```

**Testnet:**

```
bash <(curl -sSL https://tomochain.com/get-tomox-testnet.sh)
```

After finishing the command above, you can see the result:

* See fullnode in the Stats Page (Mainnet: https://stats.tomochain.com, Testnet: https://stats.testnet.tomochain.com/)
* Open your relayer on browser (http://\[SERVER\_IP])

{% hint style="info" %}
Wait until your fullnode passes the block number that you registered your relayer on to see the pairs
{% endhint %}

### Setup manually <a href="#setup-manually" id="setup-manually"></a>

#### Prerequisite <a href="#prerequisite" id="prerequisite"></a>

**Minimum hardware and software requirements**

* Processing transactions is mostly CPU bound. Therefore we recommend running CPU optimized servers.(You can check our base recommendations to create your fullnode [here](https://docs.tomochain.com/masternode/requirements/))
  * Directly facing internet (public IP, no NAT)
  * 16 cores CPU
  * 32 GB of RAM
  * SSD Storage

{% hint style="info" %}
If you are running a node in Testnet, 8CPU/32GB of RAM is sufficient.
{% endhint %}

**Application platform**

* Go 1.12 or higher
* Docker with the latest version
* Nodejs 8.16.x or higher
* Nginx

**Networks**

Your server needs to open these ports:

* 80/443 for HTTP/HTTPs
* 30303 for fullnode

**All IT systems require maintenance**

It is of the owner's responsibility to ensure over time that your node has enough:

* Disk space to store the new blockchain data
* Processing power to keep the chain operating at optimal speed
* Monitoring to be able to react quickly in case of a problem
* Security measures like fire-walling, os security patching, ssh via keypairs, etc.

### Prepare RabbitMQ, MongoDB, and TomoX fullnode[¶](https://docs.tomochain.com/masternode/tomox-sdk/#prepare-rabbitmq-mongodb-and-tomox-fullnode) <a href="#prepare-rabbitmq-mongodb-and-tomox-fullnode" id="prepare-rabbitmq-mongodb-and-tomox-fullnode"></a>

Run MongoDB and TomoX Full node:

Use this [guide](tomox-sdk.md) to run your full node and MongoDB on the server.

And run RabbitMQ:

```
docker run -d -p 5672:5672 --name rabbitmq rabbitmq:3.8
```

### Basic Deployment <a href="#basic-deployment" id="basic-deployment"></a>

#### TomoX SDK Backend <a href="#tomox-sdk-backend" id="tomox-sdk-backend"></a>

Download `tomox-sdk` binary from [TomoX-SDK Github Releases](https://github.com/tomochain/tomox-sdk/releases).

E.g:

```
wget https://github.com/tomochain/tomox-sdk/releases/download/v1.0.1-beta/tomox-sdk.v1.0.1-beta.linux.amd64 -O tomox-sdk
chmod +x tomox-sdk
```

Or you can build the binary from the source code by following the steps below:

Clone [tomox-sdk](https://github.com/tomochain/tomox-sdk.git) to your server:

`$ git clone https://github.com/tomochain/tomox-sdk.git`

Go to `tomox-sdk` and create and edit your config file.

```
cd tomox-sdk
cp config/config.yaml.example config/config.yaml
```

We have some parameter that needs to be changed.

* `exchange_address` : Your DEX coinbase (the address you use to register a DEX on TomoRelayer)
* `exchange_contract_address`  : TomoRelayer smart contract address (Mainnet: `0x16c63b79f9C8784168103C0b74E6A59EC2de4a02`,Testnet: `0xe7c16037992bEcAFaeeE779Dacaf8991637953F3`)
* `lending_contract_address`: TomoRelayer Lending smart contract address (Mainnet: `0x7d761afd7ff65a79e4173897594a194e3c506e57`)

After customizing your config, you can build SDK backend

```
cd tomox-sdk
GO111MODULE=on
go mod download
go build .
```

And run it:

```
./tomox-sdk
```

Note: `tomox-sdk` requires `./config/config.yaml` and `./config/errors.yaml` file to run the service.

To run tomox-sdk as daemon service, you can use `pm2`, `supervisord` or `systemd`.

#### TomoX SDK UI <a href="#tomox-sdk-ui" id="tomox-sdk-ui"></a>

Download the site from [TomoX-SDK-UI Github Releases](https://github.com/tomochain/tomox-sdk-ui/releases)

E.g:

```
# download
wget https://github.com/tomochain/tomox-sdk-ui/releases/download/v1.0.1-beta/tomox-sdk-ui.v1.0.1-beta.testnet.tar.gz
# uncompress
tar xvzf tomox-sdk-ui.v1.0.1-beta.testnet.tar.gz
```

Or you can build the site by following the steps below:

Clone [tomox-sdk-ui](https://github.com/tomochain/tomox-sdk-ui.git) to your server:

```
git clone https://github.com/tomochain/tomox-sdk-ui.git
```

Go to `tomox-sdk-ui` to update the `env` file:

```
cd tomox-sdk-ui
cp .env.sample .env
```

There are some parameters that need to be changed:

* `REACT_APP_ENGINE_HTTP_URL`: url backend, `http://[SERVER_IP_OR_DOMAIN]/api`
* `REACT_APP_ENGINE_WS_URL`: url websocket backend, `ws://[SERVER_IP_OR_DOMAIN]/socket`

You need to have `yarn` and `sass` to build the site, install it:

```
npm install -g yarn sass
```

Build the site:

```
cd tomox-sdk-ui
yarn install && yarn build
```

Your DEX UI is created into `./buid` directory. You can setup web server (nginx) and domain to publish your site to internet.

You can use `nginx` to serve the site.

### Setup web server (nginx) <a href="#setup-web-server-nginx" id="setup-web-server-nginx"></a>

TomoX-SDK backend run on port 8080 in the default. We can use Nginx to serve both TomoX-SDK and TomoX-SDK-UI and publish it to internet.

```
server {
    listen       80;
    server_name  _;

    root /path_to_your_tomox_sdk_ui_build;

    index index.html index.htm;

    # TomoX-SDK API
    location /api {
         proxy_set_header X-Real-IP $remote_addr;
         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
         proxy_set_header Host $host;
         proxy_pass http://localhost:8080;
    }

    # TomoX-SDK socket
    location /socket {
        auth_basic off;
        proxy_set_header Host $host;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://localhost:8080/socket;
    }

    # TomoX-SDK UI
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

After reloading `nginx` with the new configuration. You can access your DEX via `http://SERVER_IP`

### Troubleshot & FAQ <a href="#troubleshot-faq" id="troubleshot-faq"></a>

**How to secure my DEX?**

You need to setup HTTPS and INBOUND firewall for your DEX, open only SSH (22), HTTP (80), HTTPS (443), Fullnode RLPX (30303).

You can setup firewall by using software on your server or create firewall on your cloud provider.

**Why doesn't ledger work with my DEX?**

Ledger required HTTPS to work properly with your DEX. On testnet, you can only use HD path `44/60` for your ledger, path `44/889` is only supported on mainnet.

**Error: Cannot get tokens or pairs**

You need to wait for until your fullnode pass the block number that you registered your relayer to see the pairs.

In another case, might you setup TomoX-SDK backend incorrectly. You need to make sure that `exchange_address` in `config/config.yaml` file is your DEX coinbase.
