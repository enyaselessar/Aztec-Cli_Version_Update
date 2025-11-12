### Please Update Your Node To The Latest Version 2.1.2 

### 1. STOP YOUR NODE FIRST 
 
Ctrl+c 

## 2. UPDATE WITH THE COMMAND 
```
aztec-up 2.1.2
```
```
sed -i 's/latest/2.1.2/' "$HOME/.aztec/bin/.aztec-run"
```
```
aztec -V
``` 

## 3. GENERATE NEW WALLET  
```
aztec validator-keys new   --fee-recipient 0x0000000000000000000000000000000000000000000000000000000000000000
```
You will see eth public adress and bls adress

<img width="507" height="96" alt="image" src="https://github.com/user-attachments/assets/797ca104-4532-4cef-bb39-40f3aa5f59ab" />

### Note 
These are your public wallet adresses

You can find private keys of these adress inside key1.json file

#### SAVE YOUR NEW ETH WALLET AND BLS PRIVATE KEYS
```
nano ~/.aztec/keystore/key1.json 
```

#### FUND YOUR NEW ETH ADRESS WITH MINIMUM 0.2 SEPOLIA ETH 


## 4. APPROVE 200K SPENDING TO JOIN THE NETWORK

```
cast send 0x139d2a7a0881e16332d7D1F8DB383A4507E1Ea7A "approve(address,uint256)" 0xebd99ff0ff6677205509ae73f93d0ca52ac85d67 200000ether --private-key "$PRIVATE_KEY_OF_OLD_SEQUENCER" --rpc-url YOUR ETH RPC URL
```

## 5.  JOIN THE NETWORK WITH AZTEC CLI
```
aztec \
  add-l1-validator \
  --l1-rpc-urls $ETH_RPC \
  --network testnet \
  --private-key $PRIVATE_KEY_OF_OLD_SEQUENCER \
  --attester $ETH_ATTESTER_ADDRESS \
  --withdrawer $ANY_ETH_ADDRESS \
  --bls-secret-key $BLS_ATTESTER_PRIV_KEY \
  --rollup 0xebd99ff0ff6677205509ae73f93d0ca52ac85d67
```

 ##### $ETH_RPC = Your Eth Rpc URL
 ##### $PRIVATE_KEY_OF_OLD_SEQUENCER= Your old private key of sequencer(which have 200k)
 ##### $ETH_ATTESTER_ADDRESS = Newly generated eth public adress which generated in step 3
 ##### $ANY_ETH_ADDRESS = You can use either your old eth adress or new adress(any adress)
 ##### $BLS_ATTESTER_PRIV_KEY = Newly generated wallet private keys which defined in step 4.You can see your private key via below command
 ```
 nano ~/.aztec/keystore/key1.json
```

<img width="2530" height="878" alt="image" src="https://github.com/user-attachments/assets/3167805b-0f5a-46e5-84cb-cec5a27672b6" />


## START SEQUENCER

```
aztec start --node --archiver --sequencer \
  --network testnet \
  --l1-rpc-urls Eth_Sepolia_RPC \
  --l1-consensus-host-urls Eth-beacon_sepolia_RPC \
  --sequencer.validatorPrivateKeys 0xYourPrivateKey (newly generated eth wallet private key.Get this from your key1.json file) \
  --sequencer.coinbase YourAddress (Newly generated eth attester adress.Get this from step 3) \
  --p2p.p2pIp Your_ip
```

## CHECK YOUR NEW ADRESS https://dashtec.xyz/queue.

<img width="1439" height="819" alt="image" src="https://github.com/user-attachments/assets/c9ac035c-d03a-4b44-9a68-9df84f1d98ee" />
