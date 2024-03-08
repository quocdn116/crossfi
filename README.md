# install crossfi node


1. Auto Install

sudo apt install curl -y && source <(curl -s https://raw.githubusercontent.com/quocdn116/crossfi/f9cb4b5a59c940372254c3f0873eacd6e6eb123c/CrossFi)

2. Wallet Managment 

Add new wallet 

crossfid keys add wallet

Recover existing key

crossfid keys add wallet --recover

List all Key

crossfid keys list

3. Create Validator

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

4. Delegate Token to your own validator

crossfid tx staking delegate $(crossfid keys show wallet --bech val -a) 1000000000000000000000mpx --from wallet --chain-id crossfi-evm-testnet-1 --gas-prices 10000000000000mpx --gas-adjustment 1.5 --gas auto -y

5. Services Management
# Reload Service
sudo systemctl daemon-reload

# Enable Service
sudo systemctl enable crossfid

# Disable Service
sudo systemctl disable crossfid

# Start Service
sudo systemctl start crossfid

# Stop Service
sudo systemctl stop crossfid

# Restart Service
sudo systemctl restart crossfid

# Check Service Status
sudo systemctl status crossfid

# Check Service Logs
sudo journalctl -u crossfid -f --no-hostname -o cat

6. Backup your validator
cat $HOME/.crossfid/config/priv_validator_key.json

7. Remove Node

sudo systemctl stop crossfid && sudo systemctl disable crossfid && sudo rm /etc/systemd/system/crossfid.service && sudo systemctl daemon-reload && rm -rf $HOME/.crossfid && sudo rm -rf $(which crossfid) 

