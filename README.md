# Running a Proof of Authority Blockchain-

For this project, I took on the role of a new developer at a small bank, where I set up a testnet blockchain for my organization. In doing so, I set up a custom testnet blockchain, sent a test transaction, created a repository and wrote instructions on how to use the chain for the rest of your team.

## Setting the custom out-of-the-box blockchain

### The instructions for creating the genesis block and setting up the nodes are as follows:

Create accounts for two (or more) nodes for the network with a separate datadir for each using geth. 
  - ./geth --datadir node1 account new
  - ./geth --datadir node2 account new

Run puppeth, name your network, and select the option to configure a new genesis block.

Choose the Clique (Proof of Authority) consensus algorithm.

Paste both account addresses from the first step one at a time into the list of accounts to seal.

Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.

You can choose no for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.

Export genesis configurations. This will fail to create two of the files, but you only need networkname.json.

Delete the networkname-harmony.json file.

Initialize each node with the new networkname.json with geth.
  Using geth, initialize each node with the new networkname.json.
   - ./geth --datadir node1 init networkname.json
   - ./geth --datadir node2 init networkname.json

Run the first node, unlock the account, enable mining, and the RPC flag. Only one node needs RPC enabled.

Set a different peer port for the second node and use the first node's enode address as the bootnode flag.

  Run the nodes in separate terminal windows with the commands:
  
./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock

Be sure to unlock the account and enable mining on the second node!

## Connecting a crypto wallet and sending test transaction

Use the MyCrypto GUI wallet to connect to the node with the exposed RPC port.

You will need to use a custom network, and include the chain ID, and use ETH as the currency.

Import the keystore file from the node1/keystore directory into MyCrypto. This will import the private key.

Send a transaction from the node1 account to the node2 account.

Copy the transaction hash and paste it into the "TX Status" section of the app, or click "TX Status" in the popup.

Celebrate, you just created a blockchain and sent a transaction!
