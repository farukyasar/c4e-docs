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

