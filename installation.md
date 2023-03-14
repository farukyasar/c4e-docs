# Preparation
``` 
apt update && apt upgrade -y 
```

```
apt install curl iptables build-essential git wget jq make gcc nano tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y
```

# Install GO
```
ver="1.19.4"
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz"
rm "go$ver.linux-amd64.tar.gz"
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile
source $HOME/.bash_profile
go version
```


# Installation
```
MONIKER="YOUR_MONIKER_HERE"
```
```
git clone https://github.com/chain4energy/c4e-chain && cd c4e-chain
git checkout v1.1.0
make install
```
```
c4ed version --long | grep -e version -e commit
# v1.1.0
# commit: d67fd60d07b41c52977539b9fb9c0c67de23837e
```

```
wget -O $HOME/.c4e-chain/config/genesis.json "https://raw.githubusercontent.com/chain4energy/c4e-chains/main/perun-1/genesis.json"

# check genesis
sha256sum ~/.c4e-chain/config/genesis.json
# 6c736993a681a6759d3ec41550995fe04f48dd332d03375d879f3b464c6ceabf
```
# Node configuration
```
c4ed config chain-id perun-1
c4ed config keyring-backend os
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025uc4e\"/;" ~/.c4e-chain/config/app.toml
external_address=$(wget -qO- eth0.me)
sed -i.bak -e "s/^external_address *=.*/external_address = \"$external_address:26656\"/" $HOME/.c4e-chain/config/config.toml
peers="084a5c788c9c61541152192d7dfe055c153af642@5.135.141.191:26656,81a3c179ee820d291adebc215d5d1af95b887ec8@65.109.30.185:26656,3c6553a3c45477c2a9902e54069bee7109318b9d@163.172.18.144:26656,68a611fc1d17612e4de6b1232d04568ea3c20a19@77.55.216.80:26656"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.c4e-chain/config/config.toml
seeds="30e98bbcf5bb29ed4e4ff685fa8fa84fa0ddff51@tenderseed.ccvalidators.com:26008"
sed -i.bak -e "s/^seeds =.*/seeds = \"$seeds\"/" $HOME/.c4e-chain/config/config.toml
```
# Create service file
```
tee /etc/systemd/system/c4ed.service > /dev/null <<EOF
[Unit]
Description=c4ed
After=network-online.target

[Service]
User=$USER
ExecStart=$(which c4ed) start
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
```
systemctl daemon-reload
systemctl enable c4ed
systemctl restart c4ed && journalctl -u c4ed -f -o cat
```
State sync =>
