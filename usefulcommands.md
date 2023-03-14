# Key management
`Add New Key`
```
c4ed keys add wallet
```
`Recover Existing Key`
```
c4ed keys add wallet --recover
```
`List All Keys`
```
c4ed keys list
```
`Delete Key`
```
c4ed keys delete wallet
```

`Export Key (save to wallet.backup)`
```
c4ed keys export wallet
```

`Import Key`
```
c4ed keys import wallet wallet.backup
```

`Balance`
```
c4ed q bank balances $(c4ed keys show wallet -a)
```
# Token management
`Withdraw Rewards From All`
```
c4ed tx distribution withdraw-all-rewards --from wallet --chain-id perun-1 --gas-prices 0.1uc4e --gas-adjustment 1.5 --gas auto -y
```
`Withdraw Commission And Rewards`
```
c4ed tx distribution withdraw-rewards $(c4ed keys show wallet --bech val -a) --commission --from wallet --chain-id perun-1 --gas-prices 0.1uc4e --gas-adjustment 1.5 --gas auto -y 
```
`Delegate`
```
c4ed tx staking delegate $(c4ed keys show wallet --bech val -a) 10000uc4e --from wallet --chain-id perun-1 --gas-prices 0.1uc4e --gas-adjustment 1.5 --gas auto -y

```
# Service
`Reload Services`
```
sudo systemctl daemon-reload
```
`Enable Service`
```
sudo systemctl enable c4ed
```
`Disable Service`
```
sudo systemctl disable c4ed
```
`Run Service`
```
sudo systemctl start c4ed
```
`Stop Service`
```
sudo systemctl stop c4ed
```
`Restart Service`
```
sudo systemctl restart c4ed
```
`Logs`
```
sudo journalctl -u c4ed -f --no-hostname -o cat

```


