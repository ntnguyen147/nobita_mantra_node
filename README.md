# nobita_mantra_node
nobita_mantra_node

# Deploy Mantra Node with Script
```
- Step 1: 
SSH to Server and run: source <(curl -s https://itrocket.net/api/testnet/mantra/autoinstall/)
```
- Follow the script's instructions

Step 2: Create Wallet: 
- to create a new wallet, use the following command. don’t forget to save the mnemonic
```
mantrachaind keys add $WALLET
```
- to restore exexuting wallet, use the following command
```
mantrachaind keys add $WALLET --recover
```
# save wallet and validator address
WALLET_ADDRESS=$(mantrachaind keys show $WALLET -a)
VALOPER_ADDRESS=$(mantrachaind keys show $WALLET --bech val -a)
echo "export WALLET_ADDRESS="$WALLET_ADDRESS >> $HOME/.bash_profile
echo "export VALOPER_ADDRESS="$VALOPER_ADDRESS >> $HOME/.bash_profile
source $HOME/.bash_profile

# check sync status, once your node is fully synced, the output from above will print "false"
mantrachaind status 2>&1 | jq .SyncInfo

# before creating a validator, you need to fund your wallet and check balance
mantrachaind query bank balances $WALLET_ADDRESS

Step 3: Create Validator

mantrachaind tx staking create-validator \
--amount 1100000uaum \
--from $WALLET \
--commission-rate 0.1 \
--commission-max-rate 0.2 \
--commission-max-change-rate 0.01 \
--min-self-delegation 1 \
--pubkey $(mantrachaind tendermint show-validator) \
--moniker "Your_moniker" \
--identity "" \
--details "Your Operator" \
--chain-id mantrachain-testnet-1 \
--gas auto --gas-adjustment 1.5 --fees 50uaum \
-y

# note: Change Moniker and details, amount 

Step 4: After you successfully create a validator, visit https://explorer.testnet.mantrachain.io/mantrachain/validators to check node

# Staking Command
- mantrachaind tx staking delegate $(mantrachaind keys show ntnguyen --bech val -a) 1070000uaum --from ntnguyen --chain-id mantrachain-testnet-1 --node="http://127.0.0.1:21657/" --gas=auto --gas-adjustment 1.5 --fees 100uaum -y
- 
**--> You need to change your information**
# Send Token Command
mantrachaind tx bank send To_address form_address 200000uaum --gas auto --gas-adjustment 1.5 --fees 50uaum -y

EXP: mantrachaind tx bank send mantra1drpnmuqvj2u7n3lf60gfdz0lck5nj6mjjltf6y mantra1fy5z907mjs4dtwlgzukwctjahe932eakd5ak78 200000uaum --gas auto --gas-adjustment 1.5 --fees 50uaum -y





