# Join the Testnet

Make sure to have the \`go-bitsong testnet version\`.

### Install \`go-bitsong-testnet\`

#### Pre-requisites

* Ubuntu 20.04
* Golang v1.17
* Git

#### From Source

Open a new terminal and clone the `go-bitsong` repository

```
git clone https://github.com/bitsongofficial/go-bitsong.git
```

Change to the repository directory

```
cd go-bitsong
```

Checkout the `testnet` release

```
git checkout testnet
```

Install `go-bitsong`

```
make install
```

### Initialize the chain

```
bitsongd init <moniker> --chain-id=bigbang-test-2
```

### Genesis & Seeds

#### Copy the Genesis File

Fetch the testnet's `genesis.json` file into `bitsongd`'s config directory.

```
wget -O ~/.bitsongd/config/genesis.json https://raw.githubusercontent.com/bitsongofficial/networks/master/testnet/bigbang-test-2/genesis.json
```

#### **Set persistent peers**

Your node needs to know how to find peers. You'll need to add healthy seed nodes to `$HOME/.bitsongd/config/config.toml`

```
export PEERS="4336c0f749d804d77a36534fbe37e5e85606a1ff@78.47.82.185:26656"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.bitsongd/config/config.toml
```

### Background Process <a href="#background-process" id="background-process"></a>

To run the node in a background process with automatic restarts, you can use a service manager like `systemd`. To set this up run the following:

```
sudo tee /etc/systemd/system/bitsongd.service > /dev/null <<EOF  
[Unit]
Description=BitSong Network Daemon
After=network-online.target

[Service]
User=$USER
ExecStart=$(which bitsongd) start
Restart=always
RestartSec=3
LimitNOFILE=4096

[Install]
WantedBy=multi-user.target
EOF

```

Then setup the daemon

```
sudo -S systemctl daemon-reload
sudo -S systemctl enable bitsongd
```

We can then start the process and confirm that it is running

```
sudo -S systemctl start bitsongd

sudo service bitsongd status
```

### Get tokens from faucet

```
curl -X POST -d '{"address": "bitsong1......"}' https://faucet.testnet.bitsong.network
```

### Fantoken Module

#### Query fantoken params

```
bitsongd query fantoken params --node https://rpc.testnet.bitsong.network:443
```

#### Issue a new fantoken

```
bitsongd tx fantoken issue \
--name "Angelo's Fantoken" \
--symbol "angelo" \
--max-supply "1000000000" \
--issue-fee 1000000ubtsg \
--description "The most popular fantoken" \
--chain-id bigbang-test-2 \
--from user \
-b block \
--keyring-backend test \
--node https://rpc.testnet.bitsong.network:443
```

#### Query fantoken by owner

```
bitsongd query fantoken owner bitsong1dw9fdvrc46ed98rndpulem466t0zf0m2gt6zyk --node https://rpc.testnet.bitsong.network:443
```

#### Query fantoken by denom

```
bitsongd query fantoken denom ft0011B9AE260F69D60438095F95F50AF9976015A9 --node https://rpc.testnet.bitsong.network:443
```

#### Mint a fantoken

```
bitsongd tx fantoken mint ft0011B9AE260F69D60438095F95F50AF9976015A9 \
--recipient <rcpt-address> \
--amount 1000 \
--chain-id bigbang-test-2 \
--from user \
-b block \
--keyring-backend test \
--node https://rpc.testnet.bitsong.network:443
```

#### Burn a fantoken

```
bitsongd tx fantoken burn ft0011B9AE260F69D60438095F95F50AF9976015A9 \
--amount 1 \
--chain-id bigbang-test-2 \
--from user \
-b block \
--keyring-backend test \
--node https://rpc.testnet.bitsong.network:443
```

#### Edit a fantoken

**ATTENTION**: If you edit your fantoken to `--mintable false` it will no longer be possible to make it **mintable**

```
bitsongd tx fantoken edit ft0011B9AE260F69D60438095F95F50AF9976015A9 \
--mintable true \
--chain-id bigbang-test-2 \
--from user1 \
-b block \
--keyring-backend test \
--node https://rpc.testnet.bitsong.network:443
```

#### Transfer the fantoken creator ownership

```
bitsongd tx fantoken transfer ft0011B9AE260F69D60438095F95F50AF9976015A9 \
--recipient <rcpt-address> \
--chain-id bigbang-test-2 \
--from user \
-b block \
--keyring-backend test \
--node https://rpc.testnet.bitsong.network:443
```

\
