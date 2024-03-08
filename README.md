# install crossfi node

Refer to docs from here for more information

https://docs.crossfi.org/crossfi-chain/technical-information/validators 


1. Auto Install
```python 
sudo apt install curl -y && source <(curl -s https://raw.githubusercontent.com/quocdn116/crossfi/f9cb4b5a59c940372254c3f0873eacd6e6eb123c/CrossFi)
```

2. Wallet Managment 

Add new wallet

```python 
crossfid keys add wallet
```
Recover existing key
```python 
crossfid keys add wallet --recover
```
List all Key
```python 
crossfid keys list
```
3. Create Validator
```python 
crossfid tx staking create-validator \
  --amount=1000000000000000000mpx \
  --pubkey=$(crossfid tendermint show-validator) \
  --moniker="your_moniker" \
  --chain-id="crossfi-evm-testnet-1" \
  --commission-rate="0.10" \
  --commission-max-rate="0.20" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation="1000000" \
  --gas="auto" \
  --gas-prices="10000000000000mpx" \
  --gas-adjustment=1.5 \
  --from=wallet
```

Check Sync before create validator
```python
crossfid status 2>&1 | jq .SyncInfo.catching_up
```

4. Delegate Token to your own validator
```python 
crossfid tx staking delegate $(crossfid keys show wallet --bech val -a) 1000000000000000000000mpx --from wallet --chain-id crossfi-evm-testnet-1 --gas-prices 10000000000000mpx --gas-adjustment 1.5 --gas auto -y
```
5. Services Management
   
Reload Service
```python 
sudo systemctl daemon-reload
```
Enable Service
```python 
sudo systemctl enable crossfid
```
Disable Service
```python 
sudo systemctl disable crossfid
```
Start Service
```python 
sudo systemctl start crossfid
```
Stop Service
```python 
sudo systemctl stop crossfid
```
Restart Service
```python 
sudo systemctl restart crossfid
```
Check Service Status
```python 
sudo systemctl status crossfid
```
Check Service Logs
```python 
sudo journalctl -u crossfid -f --no-hostname -o cat
```
6. Backup your validator
   
```python 
cat $HOME/.crossfid/config/priv_validator_key.json
```
8. Remove Node
   
```python 
sudo systemctl stop crossfid && sudo systemctl disable crossfid && sudo rm /etc/systemd/system/crossfid.service && sudo systemctl daemon-reload && rm -rf $HOME/.crossfid && sudo rm -rf $(which crossfid) 

```

